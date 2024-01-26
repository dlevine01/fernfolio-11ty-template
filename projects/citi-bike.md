--- 
title: "Test Citi Bike’s reliability"
metaDescription: Evaluate Citi Bike availability and reliability using real-time location data and demographic equity analysis
emoji: 🚴
date: 2023-11-01T00:00:00
summary: "As riders increasingly complained of finding Citi Bike docks empty or full of broken docks, I collected and analyzed the system’s real-time station data to show patterns of poor reliability — especially in neighborhoods home to more Hispanic, Black, and lower-income residents."
tags:
- spatial analysis
--- 

### Challenge

Citi Bike riders found the system was getting less reliable. More often, riders complained of finding stations completely empty or full of broken, out-of-service bikes. 

Citi Bike touted recent expansions into new neighborhoods and additions to the electric bike fleet, but their scant data about system performance made it impossible to validate riders’ experience and find whether Citi Bike was equitably available across neighborhoods.

### Data

We needed a more granular look at where and when bikes were available across the system. Citi Bike publishes a live [data feed](https://gbfs.citibikenyc.com/gbfs/gbfs.json), to enable apps to provide up-to-the minute routing, with the detail we needed. But, by design, this data is only real-time, not historical.

So I put together a little automated [script](https://github.com/dlevine01/archive-citibike-gbfs) to fetch and stash this data and automated the process to pull down the live data every 15 minutes.

Running this data getter through two months of peak summer ridership gave us a detailed dataset with an every-fifteen-minute glimpse of the number of bikes and docks at each station.

I computed several aggregate measures for each station to measure rider experience and system reliability: 
- the frequency or likelihood, that stations were either empty (no bikes) or completely full (no docks), during morning and evening peak periods
- the durations these outages lasted (based on consecutive time samples when the number of bikes or docks remained at zero)
- the portion of docks holding broken or out-of-service bikes.

### Analysis

This station-level data could be directly compared with service level requirements in Citi Bike’s operating contract, including the maximum time allowed for stations to be left empty. Citi Bike was routinely blowing past this standard, enough to be liable for more than $800,000 in penalties just over the two months we analyzed. 

Initial mapping of the station performance measures showed obvious geographic disparities in service: bikes and docks were generally available in core areas of Manhattan, but across the outer edges of the system in Brooklyn, Queens, the Bronx and upper Manhattan, stations were more frequently unavailable and outages lasted longer. 

<div class="landscape-map-container">
    <iframe
    src="/static/files/Fig_3_frequency_unavailable.html"
    title="Frequeny stations were unavailable"
    ></iframe>
</div>

One empty or full station is a problem for riders, but when _all_ the stations across a neighborhood or area have no bikes or no docks, potential riders are stranded. If these area-wide outages are frequent, Citi Bike is no longer a reliable travel mode for riders in that area.

To find clusters of frequent poor service—and to compress the variability in station performance across different measures into an easy classification of “reliable” or “not reliable” —I used a local indicators of spatial association algorithm to pick out the stations that had exceptionally poor service (compared to citywide averages), and whose neighboring stations _also_ had poor service on the same measures. This data-driven method showed the worst clusters of stations.

In sharing these initial findings with my colleagues, a sensible question came up: what are the thresholds for what we are calling poor service? What to those levels mean for riders?

It was easy enough to find what thresholds the clustering algorithm had devised, based on the distribution of the data. But to work with my colleagues to inspect these thresholds and see what clusters of poor service are identified based on different service levels, I reworked the clustering on variable thresholds and built a little [app](https://explore-citi-bike-service-thresholds-ncd3u6yygj498rsaawg9mr.streamlit.app/) to adjust these thresholds and see what clusters are identified.

For our policy-focused research, we needed to know not just where there were service disparities, but also whether there were inequitable patterns further disadvantaging communities of color or neighborhoods with more low-income residents.

I pulled tract-level Census demographic information and aggregated race, ethnicity, and poverty rates within poor service areas, compared to the City overall and the entire Citi Bike service area. 

### Key findings

This [analysis](https://comptroller.nyc.gov/reports/riding-forward-overhauling-citi-bikes-contract-for-better-more-equitable-service/) validated riders’ experiences and found alarmingly frequent instances when bike share stations were left with no bikes or docks available. 

Moreover, it showed clear inequities: areas where all nearby stations had poor availability or long durations with no bikes or docks were neighborhoods with more Hispanic/Latino residents, more low-income residents.

Citi Bike’s failure to rebalance bikes to make docks and bikes available directly violates the service agreements in the bikeshare system’s operating contract, to the extent that Citi Bike could be liable for more that $800,000 in penalties just for the two months we analyzed. 

### Coverage

These findings on poor service and inequities earned substantial media coverage, including in the [New York Times](https://www.nytimes.com/2023/11/15/nyregion/citi-bike-riders-stations.html), [Gothamist](https://gothamist.com/news/nyc-comptroller-citi-bike-service-has-worsened-since-lyfts-2018-takeover), local [TV](https://www.cbsnews.com/newyork/news/new-report-highlights-citi-bike-shortcomings-under-lyfts-management/) [news](https://abc7ny.com/citi-bike-new-york-city-comptroller-brad-lander-bicycle/14062860/), and [Fast Company](https://www.fastcompany.com/90984006/new-yorks-comptroller-says-citi-bike-service-is-lacking-in-low-income-areas-citi-bike-disagrees).

### Skills

- applied spatial clustering to find patterns of poor service
- build a longitudinal dataset from live data with an automated data getter
- demographic analysis to show inequities in service quality
- collaborating with policy experts to hone recommendations and with communications staff to build a compelling news story
- maps!

