---
title: "Covid Alberta"
excerpt: "web scraper and data visualization scripts for looking at covid-19 data from the alberta website"
header:
  teaser: assets/images/Alberta_doublingTime_RW.png
toc: True
---

This is a small package that I have developed to look at some of the alberta specific covid data.

There are two parts to the package. the webscraper and the data analysis

## Web Scraper

The `albertaC19_websraper` is a class that scrapes the updated stats off of the [alberta Covid-19 website](https://covid19stats.alberta.ca/).

example of using the webscraper
```python
import covid_alberta
abC19 = covid_alberta.albertaC19()
abTotal, abRegion, abTesting = abC19.scrape_all(return_dataframes=True)
```

## Data Analysis

Currently I am developing the stats and plotting packages in the CovidAlberta.ipynb
I will convert it over into a more formal package with functions as I finish it up. Some of the stats I am looking at are the cumulative case increase across Alberta as well as calculating the doubling rate of the case counts.

example for calculating the stats

```python
region_dt = calculate_doublingtimes(abRegion, col_suffix='cumulative', combine_df=False)
total_dt = calculate_doublingtimes(abTotal, col_suffix='cum_cases', combine_df=False)

all_data = abTotal.join([total_dt, abRegion, region_dt, abTesting])
```

I have seen a lot of graphs showing the cumulative curve with as well as the "2, 3, and 4 day doubling rate" curves. Which made me think, why not just calculate that rate? If you calculate the actual doubling rate you can start looking at some interesting things such as how our doubling rate is changing compared to the cumulative case count? Here's an example of that image.

<!-- <iframe id="igraph" scrolling="no" style="border:none;"
seamless="seamless"
src="/assets/images/Alberta_doublingTime_RW.html"
alt="Doubling Time by Case Count"
height="525" width="100%"></iframe> -->

{% include posts_images/2020/doubling_time.html %}

I have also been seeing a lot of plots lately showing the cumulative case counts which only tells part of the story. I decided to create another plot where I could look at case counts alongside the daily number of tests. This gives me an idea if how much to possibly trust the daily increase number.

{% include posts_images/2020/daily_cases.html %}
