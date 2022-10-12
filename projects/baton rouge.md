---
title: Help a redevelopment agency choose where to build housing and where to restore flood-mitigating green space
emoji: 🏡
metaDescription: model stormwater risk 
date: 2022-08-20T00:00:00.000Z
summary: As Baton Rouge faces greater flood risk, escalating housing costs, and unequal growth, this project helps the region’s urban redevelopment agency choose which of its properties to redevelop as affordable housing and which to convert to stormwater-absorbing green spaces.
tags:
  - program development
  - spatial analysis
  - green infrastructure
---
![Baton Rouge modeled flood risk](/static/img/retention-close-up.png)

## Challenge
Baton Rouge faces growing flood risk from climate change and challenges from rapid growth and escalating housing costs as the region’s population booms. However, core parts of the city still suffer from divestment. Build Baton Rouge was recently formed as a redevelopment agency tasked with revitalizing neighborhoods by improving vacant, abandoned, and deteriorating properties. To help the region grow sustainably, the agency needs to select which parcels to develop as new affordable housing and which sites to repurpose as parks and green spaces that can be nature-based buffers against stormwater. 

## Mapping and analysis
To help kick off this applied research project, I modeled the physical flood risk across the Amite River basin. Using the [InVEST](https://naturalcapitalproject.stanford.edu/software/invest) urban stormwater model. I created high-resolution views of the specific flood vulnerability at each location across the region.

## Insights
Modelling the stormwater runoff in a heavy rainstrom shows that the lower basins of the Amite River—in the neighborhoods of southern and eastern Baton Rouge—generate the most intense flood runoff. 

![subbasin map](/static/img/Amite-basins-flood-risk-intensity.png)
_Stormwater flood generation intensity is greatest in the lower subbasins of the Amite River_

The northern watersheds of the Amite River, meanwhile, have the most potential to absorb rainwater in heavy storms (and thereby reduce downstream flooding). These areas are still predominantly rural, but face pressure for new development which could destroy the natural absorbent landscape. 

![strormwater retention](/static/img/stormwater-retention.png)
_More stormwater is retained in the northern subbasins_

### Context
The Baton Rouge region sits inland from the Gulf shore but is affected by coastal storms and by inland flooding of the Amite River. The oldest part of the city sits on relatively high ground, but many of these neighborhoods have faced divestment, while the in-migration to the area (including a population forced to retreat from flood-ravaged coastal areas) has spread out from the city core, into low-lying and more risky areas. Devastating floods in recent years have highlighted the risk of this development and the threat to new residents unwittingly sold homes in hazardous areas, while at the same time growth across the region has jacked up home values and made affordable housing a more urgent concern.
 
Build Baton Rouge is a land bank agency that takes title of vacant, abandoned, or deteriorated properties and looks for opportunities to redevelop them in ways that will strengthen their neighborhoods and reverse local economic declines. This project will support the agency’s decisions on where to redevelop parcels as affordable housing and where to build parks and restore green spaces that can mitigate stormwater flood risk.

 Aggregating to the subbasin level shows that the lower watersheds, closest to the core of Baton Rouge, generate the most intense stormwater runoff, while the northern tributaries (which are still rural but under development pressure) are naturally retaining the most water in heavy rain events. 

#### Technical nitty gritty
The [InVEST](https://naturalcapitalproject.stanford.edu/software/invest) tool models an array of “ecosystem services,” or ways the natural environment supports the build landscape and economy. The urban stormwater model depends on spatial data for land use/land cover and soil hydrology types, as well as locally validated measures relating each land cover type to an amount of permeability. 

I sourced land use/land cover and soil survey data from STAC assets hosted on the Microsoft Planetary Computer. This interface allows for pulling data for any area of influence, so the analysis could be easily replicated anywhere in the U.S. (with adjustments for local relationships between land cover and permeability). It also pulls data directly into a Python workflow; I merged, reclassified, and reprojected the data using `rasterio`, `rioxarray`, and `numpy` tools. Check out the code [here](https://colab.research.google.com/drive/1RV-HEE5J1C8yNyyMiHYI3JwpDa_SmBFd?usp=sharing) and [here](https://colab.research.google.com/drive/1gbfuoIYX6vIFBxBqakKXGJFM0jFYyanp?usp=sharing).

### Next steps 
Working with colleagues on the project, I began to aggregate this physical flood hazard with measures of social vulnerability and records of vacant properties and planned property development. Together, these multiple factors can inform development decisions for Build Baton Rouge and other policy makers in the region about the best areas to develop and the areas where nature-based flood protection and economic development will together be most important.

##### Skills

- raster data manipulation in Python
- STAC API to access raster data assets sourced from satellite imagery and land surveys
- InVEST model to predict stormwater flooding