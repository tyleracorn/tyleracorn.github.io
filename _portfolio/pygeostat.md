---
title: "pygeostat"
excerpt: "A geostatistical workflow package used to manage and visualize geostatistical workflows that use the GGLIB software"
header:
  teaser: http://www.ccgalberta.com/pygeostat/_images/pygeostat_logo.png
toc: True
---
pygeostat is a Python 3.6 module for geostatistical modeling. pygeostat is aimed at preparing spatial data, scripting geostatistical workflows, modeling using tools developed at the Centre for Computational Geostatistics, and constructing visualizations to communicate spatial data.

## Features:

* Configurations of persistent project parameters and plotting style parameters
* Data file management functions for interacting with CSV, GeoEAS (GSLIB), and VTK formats
* Utilities for managing GSLIB-style grid definitions
* Export gridded and point data files for visualization with Paraview (VTK format)
* Simplified scripting of gslib programs with parallelization and crash detection/notification
* Linear desurveying and compositing methods including automatic composite detection
* Fast, accurate variogram calculation, model fitting and modeling routines
* Vast library of plotting functions

If you are interested for now you can head over to the [pygeostat homepage](http://www.ccgalberta.com/pygeostat/). A public version is not currently available due to wrapping of proprietary Fortran code in the package. However, there are rumors of a public version coming soon.
