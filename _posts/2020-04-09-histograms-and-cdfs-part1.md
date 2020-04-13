---
title: "Histograms and CDF's Part1: What are they?"
excerpt: "At their heart, both the Histogram and the CDF (Cumulative Distribution Function) are displaying similar information, but in different ways. The Histogram (or PDF) represents the probability with areas. The CDF represents probability with vertical distances."
categories:
  - statistics
tags:
  - statistics
  - histogram
  - cdf
  - distributions
  - definitions
last_modified_at: 2020-04-09
toc: true
---

This is the first post is a series talking about histograms and CDF's. I find a lot of people new to data science, geostatistics, etc. are usually familiar and comfortable with histograms, however there is a lot to learn from CDF's which is why I tend to rely on them more. This series will cover the following topics

1. What are they?
    - Defining the histogram and the cdf

2. What do they tell us?
    - Looking at what info we can easily read from each graph type

3. When should we use them?
    - What are the pro's and con's of these graphical representations.

## TL:DR

A histogram can be thought of as an empirical estimation of the Probability Density Function (PDF). At their heart, both the PDF and the CDF (Cumulative Distribution Function) are displaying similar information, but in different ways. The Histogram (or PDF) represents the probability with areas. The CDF represents probability with vertical distances.

## Histogram

Histograms are one commonly used graphical representation of a distribution of numbers. They are typically plotted in a bar graph style plot where the height of each bar shows the frequency of a bin and represents the probability that a number will fall within that bin. The width of the bar represents the bin size used to group the numbers. The total width of all bars shows the range of values in the distribution. Here's an example:

![histogram](/assets/images/normal_histogram.png){:width="300px"}

The histogram can also be thought of as an empirical estimate of the probability density function (PDF). You can estimate that and see what that might look here.

![histogram_pdf](/assets/images/normal_histogram_pdf.png){:width="300px"}

<!-- <p align="center">
  <img width="200" src="/assets/images/normal_histogram.png">
</p> -->

## CDF

The cumulative distribution function (aka. CDF) is another graphical representation of the distribution of numbers (discrete, or continuous). The y-axis represents the cumulative probability, aka the percentile of your distribution. The x-axis is the values in your distribution (ordered from least to greatest).

![cdf](/assets/images/normal_cdf.png){:width="300px"}

So looking at the above cdf we can see some points. draw a line from 0.5 over to your cdf and then go straing down, that's the median of your distribution (Here it's 14.4). If you do the same at 0.8 that's the P80. In this example we can see that 80 percent of the values in this  distribution are less than or equal to 17.2.

If you want to see how I made the above plots in python you can check out my example notebook [ex_histograms_and_cdfs](https://github.com/tyleracorn/lessons/blob/master/Ex_histograms_and_CDFs.ipynb)

## How do we read Histograms

Now that we know what they are......

![histogram](/assets/images/normal_histogram.png){:width="300px"}

## How do we read CDF's

Now that we know what they are.....

![cdf](/assets/images/normal_cdf.png){:width="300px"}

## Pro's and Con's TL:DR

In a nutshell.

## Pro's and Con's of Histogram

Why do we so often use the histogram

## Pro's and Con's of the CDF

When we should be using the CDF.
