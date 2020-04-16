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
toc_sticky: true
---

This is the first post is a series talking about histograms and CDF's. I find a lot of people new to data science, geostatistics, etc. are usually familiar and comfortable with histograms, however there is a lot to learn from CDF's which is why I tend to rely on them more. This series will cover the following topics

1. What are they?
    - Defining the histogram and the cdf

2. What do they tell us?
    - Looking at what info we can easily read from each graph type

3. When should we use them?
    - What are the pro's and con's of these graphical representations.

## TL:DR

At their heart, both the histogram and the CDF (Cumulative Distribution Function) are displaying similar information, but in different ways. A histogram can be thought of as an empirical estimation of the Probability Density Function (PDF) and represents the probability with areas (i.e. area under the curve). The CDF represents probability with vertical distances and is cumulative.

## What's a Histogram

Histograms are one commonly used graphical representation of a distribution of numbers. They are typically plotted in a bar graph style plot where the height of each bar shows the frequency of a bin and represents the probability that a number will fall within that bin. This is in essence a slice of the area under a curve. The width of the bar represents the bin size used to group the numbers (or the width of the slice). The total width of all bars shows the range of values in the distribution. Here's an example showing the histogram and the estimated PDF:

<img src="/assets/images/2020/normal_histogram_pdf.png" style="max-width:300px" alt='histogram_pdf'>

## What's a CDF

The cumulative distribution function (aka. CDF) is another graphical representation of the distribution of numbers (discrete, or continuous). The y-axis represents the cumulative probability, aka the percentile of your distribution. The x-axis is the values in your distribution (ordered from least to greatest). The line is using vertical distances to show the probabilities.

<img src="/assets/images/2020/normal_cdf.png" style="max-width:300px" alt='cdf'>

## How do we read a Histograms

Now that we know what they are......

<img src="/assets/images/2020/normal_histogram_annotated.png" style="max-width:300px" alt='histogram annotated'>

## How do we read a CDF's

Now that we know what a CDF is, lets start looking at what sort of information one can glean from this graph. First plot up our CDF again, but with some annotations.

<img src="/assets/images/2020/normal_cdf_annotated.png" style="max-width:300px" alt='cdf'>

So looking at the above cdf we can see some points. We drew a line from 0.5 over to our cdf line and then went straight down, that's the median of our distribution (Here it's 14.4). If you do the same at 0.8 that's the P80. So, in this example we can see that 80 percent of the values in this distribution are less than or equal to 17.2.

What about the slope of the line? That in affect tells us how spread out values are. A steeper slope means that the there is less spread and a shallower slope gives shows a greater relative spread in your data.

## Pro's and Con's TL:DR

In a nutshell.

### Differences between distributions

Here is where the histogram excels. It is much easier to see differences between distributions when looking at the histogram. When comparing shapes, our brains are much better at picking out differences in something like a histogram. Because our brain is much better at picking out general differences in areas of a distribution (there tends to be greater differences in the area), where as the CDF is showing the differences between distributions by changes in the slope of the line. This tends to be a much smaller relative difference and is hard for us to pick out. Here's some examples:

<img src="/assets/images/2020/compare_hist_cdf_Beta.png" style="max-width:700px" alt='Beta'>

<img src="/assets/images/2020/compare_hist_cdf_Binomial.png" style="max-width:700px" alt='Binomial'>

<img src="/assets/images/2020/compare_hist_cdf_Chisquare.png" style="max-width:700px" alt='ChiSquare'>

<img src="/assets/images/2020/compare_hist_cdf_Gamma.png" style="max-width:700px" alt='Gamma'>

<img src="/assets/images/2020/compare_hist_cdf_Lognormal.png" style="max-width:700px" alt='Log Normal'>

<img src="/assets/images/2020/compare_hist_cdf_Poisson.png" style="max-width:700px" alt='Poisson'>

<img src="/assets/images/2020/compare_hist_cdf_Triangular.png" style="max-width:700px" alt='Triangular'>

<img src="/assets/images/2020/compare_hist_cdf_Uniform.png" style="max-width:700px" alt='Uniform'>

### Probability of a value occurring

With a histogram it is easy to see what the probability of a value occurring within a bin is. You just go to the bin in question and see what the hight is. Where things become harder is if you are interested in the probability of a value occurring within a range, say between 10 and 15, or what values would you expect between two percentiles, i.e. what values are greater than your P20 and less than your P80. With the Histogram you have to add the probabilities for all the bins in that range.

For all of the above questions, looking at the CDF you at most have to do two calculations. Each point on the line is the probability that a value is less than or equal to that point. So if you are looking at any ranges, you find the point representing the top limit of your range and subtract from it the point representing the bottom range. So for example we can see that 30% of the values lie between 14.4 and 17.2.

### Seeing Outliers

With a histogram you look at the edges of the graph to see if we have an gaps in our bins. As long as we were reasonably smart in picking our bin sizes (and didn't say pick 4 bins for 1000 data points) then it is usually relatively easy to pick out outliers in a histogram.

Outlies in the CDF are shown when you have a relatively flat section. Here it's not too bad for picking out outliers, but probably not as easy as the histogram.

## Example Script

If you want to see how I made the above plots in python you can check out my example notebook [ex_histograms_and_cdfs](https://github.com/tyleracorn/lessons/blob/master/Ex_histograms_and_CDFs.ipynb)
