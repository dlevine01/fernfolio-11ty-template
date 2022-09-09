---
title: Help choose where to develop affordable housing and where to build stormwater-absorbing green infrastructure
emoji: 🏡
metaDescription: model stormwater risk 
date: 2022-08-20T00:00:00.000Z
summary: Help an urban redevelopment agency in flood-affected Baton Rouge decide which of its properties to redevelop and which to convert to flood-absorbing green spaces.
tags:
  - program development
  - spatial analysis
  - green infrastructure
---
![Baton Rouge modeled flood risk](/static/img/BR-flood-risk-model.png)

# 

### Project context
The Baton Rouge region sits inland from the Gulf shore but is affected by coastal storms and by inland flooding of the Amite River. The oldest part of the city sits on relatively high ground, but many of these neighborhoods have faced divestment, while the in-migration to the area (including a population forced to retreat from flood-ravaged coastal areas) has spread out from the city core, into low-lying and more risky areas. Devastating floods in recent years have highlighted the risk of this development and the threat to new residents unwittingly sold homes in hazardous areas, while at the same time growth across the region has jacked up home values and made affordable housing a more urgent concern.

Build Baton Rouge is a land bank agency that takes title of vacant, abandoned, or deteriorated properties and looks for opportunities to redevelop them in ways that will strengthen their neighborhoods and reverse local economic declines. With a portfolio across the city, it is important to understand where the best locations are to redevelop as affordable housing and which are more valuable places to restore green spaces that can serve as park and neighborhood spaces and can also mitigate stormwater flood risk.

## Mapping and analysis

To help kick off this research project, I modeled the physical flood risk across the Amite River basin. Using the [InVEST] urban stormwater model I created high-resolution views of the specific flood vulnerability at each location across the region. Aggregating to the subbasin level shows that the lower  watersheds, closest to the core of Baton Rouge, generate the most intense stormwater runoff, while the northern tributaries (which are still rural but under development pressure) are naturally retaining the most water in heavy rain events. 

### nitty gritty
The [InVEST] tool models an array of “ecosystem services,” or ways the natural environment supports the build landscape and economy. The urban stormwater model depends on spatial data for land use/land cover and soil hydrology types, as well as locally validated measures relating each land cover type to an amount of permeability. 

I sourced land use/land cover and soil survey data from STAC assets hosted on the Microsoft Planetary Computer. This interface allows for pulling data for any area of influence, so the analysis could be easily replicated anywhere in the U.S. (with adjustments for local relationships between land cover and permeability). It also pulls data directly into a Python workflow; I merged, reclassified, and reprojected the data using `rasterio`, `rioxarray`, and `numpy` tools. Check out the code [here].

### Next steps 
Working with colleagues on the project, I began to aggregate this physical flood hazard with measures of social vulnerability and records of vacant properties and planned property development. Together, these multiple factors can inform development decisions for Build Baton Rouge and other policy makers in the region about the best areas to develop and the areas where nature-based flood protection and economic development will together be most important.

##### Skills

- raster data manipulation in Python
- STAC API to access raster data assets sourced from satellite imagery and land surveys
- InVEST model to predict stormwater flooding