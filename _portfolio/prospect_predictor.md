---
title: "Prospectivity Predictor"
excerpt: "This is a simple prospectivity prediction package that predicts the
prospectivity of an element based on how close it is to different
bedrock units."
header:
  teaser: assets/images/predictionHeatMap_projectBoundary.png
toc: True
---

# prospectPredictor

This is a simple prospectivity prediction package that predicts the
prospectivity of an element based on how close it is to different
bedrock units.

## Overview of Package

The package utilizes 3 main classes.

- PrepShapes
-- handles exploring and prepping a shapefile and determining the project boundary. It can read in a single shapefile (using geopandas) and then you can use it to select the polygons of interest.
- RasterTemplate
-- uses the previously initialized *PrepShapes()* class to help you setup the raster template used by the predictor to predict prospectivity at a specified location.
- PredictByDistance
-- the predictor class that predicts the likelihood based on distance to shapes of interest and the weighting schema architect. The predictor class uses the previously initialized PrepShapes() and RasterTemplate() classes. Only one prediction architect is currently implemented.

### Prediction Weighting Schema

Currently this package uses a pseudo variogram style weighting schema with the following model (for location *i* and as an example 2 distances)

.. image:: CodeCogsEqn.gif
![variogram equation](https://github.com/tyleracorn/prospectPredictor/raw/master/CodeCogsEqn.gif "variogram equation")

### Generating a prospectivity heat map

Using the package you can generate a heat map with liklihood of finding the element (based on a distance from 2 or more shape categories). The predictor generates prediction values ranging from 0, being least likely (i.e. 0%), to 1, being most likely (i.e. 100%). As an example here is a heat map generated from the included dataset.

![Prediction Heat Map](assets/images/predictionHeatMap_projectBoundary.png "Prediction Heat Map")

### Example

An example.ipynb is included in the repo to demostate how to use the package.

### Dataset
the included dataset is from the `British Columbia Geological Survey <https://www2.gov.bc.ca/gov/content/industry/mineral-exploration-mining/british-columbia-geological-survey>`.
