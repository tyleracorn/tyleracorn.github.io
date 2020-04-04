---
title: "Setting up jekyll for github pages"
categories:
  - jekyll
tags:
  - github
  - jekyll
  - github pages
last_modified_at: 2020-03-15
toc: true
---

The main point of this post is to
1. record some of the settings and theme settings I've used for setting up my github.io page.
2. include some of the development commands I always forget!

So right off the bat:

## Development Cheat Sheet
I always forget these and have to look them up. So I figured, why not just stick it here!

To start a local jekyll server so you can test changes made to your github pages open up an anaconda prompt and use the following command

`bundle exec jekyll serve`

This will load up a server and you can then access your site either at `localhost:4000` or at the ip address listed in the anaconda prompt. That's usually located at `http://127.0.0.1:4000`

## Including Interactive Plots

So I have just started playing around with [plotly](https://plotly.com/), which is a fairly nice package for creating interactive plots. It turns out that despite all of the weird convoluted rabbit trails I went down, it is actually fairly simple to create and imbed a plotly figure into your post.

First: Create the figure. For me that was using the following bit of python code

```python
fig = go.Figure()
# do all your plotting stuff
fig.write_html('plotly_test.html')
```


Second: Imbed the figure. The simplest way I found was to use the html iframe tag with some parameters to make it look nice. Here's the bit of code to add to your markdown file.

```
<iframe id="igraph" scrolling="no" style="border:none;"
seamless="seamless"
src="/assets/images/plotly_test.html"
alt="Cumulative Case Counts"
height="525" width="100%"></iframe>
```

After you have dropped the html file you created into your image folder, and linked to it in the above iframe. you'll get a beautiful interactive plot such as this one!

<iframe id="igraph" scrolling="no" style="border:none;"
seamless="seamless"
src="/assets/images/plotly_test.html"
alt="Cumulative Case Counts"
height="525" width="100%"></iframe>
