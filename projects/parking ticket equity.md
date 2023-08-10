---
title: Search for inequities in parking tickets
emoji: 🚗
date: 2023-05-01T00:00:00.000Z
summary: Search inequities in where New Yorkers get parking tickets
tags:
- spatial analysis
- policy evaluation
- data engineering
---

<!-- map here. -->

### Challenge

An elected city partner asked our office to check on patterns of inequity on where the City wrote parking tickets. Were certain disadvantaged neighborhoods particularly targeted by ticketing or getting more than their fair share of tickets?

### Data and analysis

For a relatively straightforward question, preparing the data and structuring the analysis were no small feat.

##### Geocoding

The City’s Department of Revenue publishes on NYC Open Data records of [all parking tickets](https://data.cityofnewyork.us/City-Government/Parking-Violations-Issued-Fiscal-Year-2023/pvqr-7yc4/data)—some 12 million per year—but these records are not geolocated to a point on the map. So the first step for any geographic analysis was to convert locations that could look like:

```csvpreview {header="true"}
Violation County,House Number,Street Name,Intersecting Street
NY,,W 28TH ST,CHELSEA PK
NY,436,27TH DR,
Q,,B 97 ST,SHORE FT PKWY
K,60,FURMAN ST,

```
to actual mappable locations.

The City’s Department of City Planning maintains [Geosupport](https://www.nyc.gov/site/planning/data-maps/open-data/dwn-gde-home.page), a custom geocoding tool for New York City addresses. On the one hand, this is a much more exacting tool than a familiar Google Maps free search field or geocoder tools like ESRI’s or HERE’s. But, it knows how to handle quirky New York City addresses, like Queens house numbers with dashes in the middle, or repeated street names. It also returns not just point locations, but also other administrative geographies, like Community District, Census Tract, Police Precinct, and street segment code, and projected X/Y point locations.

Geosupport takes structured queries for addresses or locations and returns only exact matches; it doesn’t interpolate addresses or guess and similar street names (it can return ‘similar’ street names but this is fairly worthless in practice. Though I am interested at some point in trying [geosupport-suggest](https://github.com/ishiland/geosupport-suggest)), but for an analytic purpose like this one, this can be an advantage: I lose some data that is not geocoded, but I can be confidant that the records I do have are where they say they are.

Actually running addresses through Geosupport, especially 50 million or so records, took some data engineering:

I used the [python-geosupport](https://python-geosupport.readthedocs.io/en/latest/) binding to include the search within a Python data pipeline. I needed to do lots of data cleaning up front to clean up addresses, then send addresses through either the house number-street addresse search or street name-other street name intersection search, depending on what information was available. Once I had a working pipeline, I had to scale it up by parallelizing the search (which is surprisingly computationally intensive) and managing memory to run the whole thing on my City-issued computer. So a few overnights later, I had point locations and relevant neighborhoods and Census Tracts for ~80 percent or so of the tickets that could be located.

Finally, I joined together the geographic locations, original ticket data, loaded everything into a sqlite database, and then I had something to work with. 

##### Building proxy measures

The analysis question was, essentially, about _which_ New Yorkers are targeted for parking tickets. This was not information we had. (Though I took some ultimately fruitless steps to try to get vehicle registration addresses to match with license plate data). Instead I had _where_ tickets were issued. This is an imperfect proxy but I tried to make it a better measure by:
1) filtering to tickets issued to New York State-registered vehicles;
2) filtering to tickets issued not on commercials streets (that is, spatially filtering to exclude tickets on streets within or adjacent to commercial or commercial overlay zoning)
3) removing certain categories of tickets that would not effect residents (e.g. missing bus permit)
4) normalizing the number of tickets in each tract by the number of households with one or more vehicle. This normalized rate I considered to be parking ticket _risk_. 
###
#### Analysis

I looked for patterns of inequity in a variety of ways. I began by looking for relationships between racial demographics of each Census Tract and the parking ticket risk. I found overall no comprehensive relationship between any racial makeup and ticket risk, but exploring geographically I found that this is because there are some predominantly Black and/or Latinx/Hispanic areas that have _higher_ ticket risk, but also some such neighborhoods with _low_ ticket risk. While race alone does not explain the variability in ticketing, this analysis did pick out certain communities of color that do have increased ticketing.

I also considered income and looked for relationships between an area’s median income or portion of residents who are poor or lower income and ticketing risk. This, again, yielded no overall, citywide pattern.

Additionally, I looked at median income or poverty status specifically of _drivers_, to better model specifically where higher ticketing risk might ensnare lower-income residents who depend on a car to get to work. I found a signs of a relationship here, where areas where a higher portion of drivers-to-work were lower income also had a higher ticketing risk. However, checking further to try to confirm this finding I found that the high margins of error on this narrow crosstab cut of Census ACS data were so large that they swamped whatever illusory effect I initially found. 

### Data visualization

![parking tickets data visualization](/static/img/parking-tickets-demo-screenshot.png)

Without a slam-dunk statistical finding, it was clear that a better way to share these data would be through a multi-faceted visualization that would allow both our initial partners and other interested data explorers to locate what would be most meaningful for them. 

I built an [interactive map and data dashboard](https://parking-tickets-demo.onrender.com) that allows crossfiltering of the data by type, timeline, and geography. Data explorers can select a neighborhood or individual Census Tract, select different types of parking tickets, and see patterns of ticketing over time as well as the comparative demographics of the area. 
