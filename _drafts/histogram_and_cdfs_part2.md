---
title: "Histograms and CDF's Part2: When Should we Use them?"
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

This is the first part of a two part series on histograms and CDF's. I find a lot of people new to data science, geostatistics, etc. are usually familiar and comfortable with histograms, however there is a lot to learn from CDF's which is why I tend to rely on them more. This series will cover the following topics

1. What are they?
    - Explain what a Histogram and CDF is
    - Show what info we can easily read from each graph type

2. When should we use them?
    - What are the pro's and con's of these graphical representations.

## Pro's and Con's TL:DR

In a nutshell.

### Differences between distributions

Here is where the histogram excels. It is much easier to see differences between distributions when looking at the histogram. When comparing shapes, our brains are much better at picking out differences in something like a histogram. Because our brain is much better at picking out general differences in areas of a distribution (there tends to be greater differences in the area), where as the CDF is showing the differences between distributions by changes in the slope of the line. This tends to be a much smaller relative difference and is hard for us to pick out. Here's some examples:

<img src="/assets/images/2020/compare_hist_cdf_Beta.png" style="max-width:700px" width="100%" alt='Beta'>

<img src="/assets/images/2020/compare_hist_cdf_Binomial.png" style="max-width:700px" width="100%" alt='Binomial'>

<img src="/assets/images/2020/compare_hist_cdf_Chisquare.png" style="max-width:700px" width="100%" alt='ChiSquare'>

<img src="/assets/images/2020/compare_hist_cdf_Gamma.png" style="max-width:700px" width="100%" alt='Gamma'>

<img src="/assets/images/2020/compare_hist_cdf_Lognormal.png" style="max-width:700px" width="100%" alt='Log Normal'>

<img src="/assets/images/2020/compare_hist_cdf_Poisson.png" style="max-width:700px" width="100%" alt='Poisson'>

<img src="/assets/images/2020/compare_hist_cdf_Triangular.png" style="max-width:700px" width="100%" alt='Triangular'>

<img src="/assets/images/2020/compare_hist_cdf_Uniform.png" style="max-width:700px" width="100%" alt='Uniform'>

### Probability of a value occurring

With a histogram it is easy to see what the probability of a value occurring within a bin is. You just go to the bin in question and see what the height is. Where things become harder is if you are interested in the probability of a value occurring within a range, say between 10 and 15, or what values would you expect between two percentiles, i.e. what values are greater than your P20 and less than your P80. With the Histogram you have to add the probabilities for all the bins in that range.

<img src="/assets/images/2020/normal_histogram_annotated.png" style="max-width:300px" width="100%" alt='histogram annotated'>

<img src="/assets/images/2020/normal_cdf_annotated.png" style="max-width:300px" width="100%" alt='cdf'>

For all of the above questions, looking at the CDF you at most have to do two calculations. Each point on the line is the probability that a value is less than or equal to that point. So if you are looking at any ranges, you find the point representing the top limit of your range and subtract from it the point representing the bottom range. So for example we can see that 30% of the values lie between 14.4 and 17.2.

### Seeing Outliers

With a histogram you look at the edges of the graph to see if we have an gaps in our bins. As long as we were reasonably smart in picking our bin sizes (and didn't say pick 4 bins for 1000 data points) then it is usually relatively easy to pick out outliers in a histogram.

<img src="/assets/images/2020/normal_histogram_pdf.png" style="max-width:300px" width="100%" alt='histogram_pdf'>

<img src="/assets/images/2020/normal_cdf.png" style="max-width:300px" width="100%" alt='cdf'>

Outliers in the CDF are shown when you have a relatively flat section. Here it's not too bad for picking out outliers, but probably not as easy as the histogram.

## Summary

CDF's are great tools for rounding out our understanding of the data. There are definitely things that are easier to pick out with a histogram versus a CDF but there are also many things I find I lose when just looking at the histogram. I find that I always end up plotting both for my data. I do rely mostly on the CDF when I am comparing two distribution (such as the distribution of my original data versus my modelled data).

## Example Script

If you want to see how I made the above plots in python you can check out my example notebook [ex_histograms_and_cdfs](https://github.com/tyleracorn/lessons/blob/master/Ex_histograms_and_CDFs.ipynb)
