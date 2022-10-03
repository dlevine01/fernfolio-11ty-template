---
title: Measure inequity in tree canopy change
emoji: 🍃
metaDescription: Tree canopy equity analysis in New York City
date: 2022-04-01T00:00:00.000Z
summary: Use high-resolution data to measure tree canopy change across New York City and use analysis tools to evaluate equity. 
tags:
  - spatial analysis
  - data engineering
  - green infrastructure
---
![tree canopy ~ heat vulnerability](/static/img/tree-canopy-analysis-1.png)

### Challenge
Extreme heat is one of the most dangerous weather events and an increasing threat under climate change. Tree cover provides shade and absorbs heat, blunting some of the effects of the ‘urban heat island.’ New York City’s MillionTrees campaign added trees citywide.

Did new tree cover reach the neighborhoods with the greatest vulnerability to extreme heat?

Using high resolution LiDAR-sourced tree cover data, this project assessed whether the changes in tree cover were equitable.

![NYC LiDAR](/static/img/LiDAR.jpg)

By mapping and modeling local tree gain (or loss) against neighborhood demographics, the study found trends and local outliers.

### Insights 
![tree canopy change analysis maps](/static/img/tree-canopy-analysis-annotated.png)
1. In general, areas with greater heat vulnerability also saw the most gain in tree cover (good news!). The correlation is particularly strong in the south and central Bronx, and in parts of East New York, neighborhoods with high heat vulnerability that have seen some of the greatest gains in tree cover.
2. Interestingly, the relationship is inverted in lower Manhattan, which has also seen a substantial gain in tree cover, but has low vulnerability. 

![tree canopy gain ~ moved since 2005](/static/img/tree-canopy-households-moved.png)

3. One way to measure neighborhood change is by the portion of residents who have more recently moved into their current home. The portion of newly arrived residents is most positively associated with increased tree canopy gain in Williamsburg, Bushwick, and the middle west side of Manhattan (with an especially strong correlation near the Williamsburg waterfront). That these transforming areas have seen more tree cover could indicate that more trees are added in gentrifying areas, or that as areas are converted from industrial to residential zones, tree canopy is increased. 

##### Nitty gritty

Check out the code notebooks and full technical report [here](https://github.com/dlevine01/nyc-tree-canopy/).

##### Skills

- Python pipeline to process LiDAR data and join demographic and economic indicators
- testing and mapping relationships with geographically weighted regression
- computing forest connectedness using fractal dimension