---
layout: default
title: Extending COMOKIT
nav_order: 4
permalink: /setupYourOwn
---

# Extending COMOKIT
{: .no_toc }


How to apply COMOKIT to your own dataset
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Requirements

You need to have a GAMA with COMOKIT installed and running. If it not yet the case, please refer to the [previous documentation page](gettingStarted)

## Data

In order to declare or apply an experiment to a new case study, COMOKIT requires a minimal dataset that should be, at least, composed of:

> You can find examples of these datasets in the [default datasets](https://github.com/COMOKIT/COMOKIT-Model/tree/master/COMOKIT/Datasets) included in COMOKIT (folder `COMOKIT/Datasets` in your workspace) or [online here](https://github.com/COMOKIT/COMOKIT-Model/tree/master/COMOKIT/Datasets)

- Spatial data:
  - **boundary.shp** *[Required]*  : this file should contain the boundary of the case study. _It is the only file absolutely required_ to define a new case study. 
  - **buildings.shp** *[Optional]* : this file should contain the buildings of the case study. Buildings are in COMOKIT the places where peoples' activities are held. The shapefile attributes table should contain a column named `type` containing the type of the building according to the [OSM specifications](https://wiki.openstreetmap.org/wiki/Map_Features#Building). If buildings are not available for the case study, COMOKIT proposes a model (in `COMOKIT/Utilities/Generate GIS Data.gaml`) that requests OSM servers with respect to the area defined in `boundary.shp` and attempts to build the `buildings.shp` file automatically. This short video will guide you through this process: 

<iframe width="560" height="315" src="https://www.youtube.com/embed/sQI63mgtYi4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- Demographic data : 
  - **population.csv** *[Optional]* : a file that contains individual including some basic attributes, i.e. age, gender and household identifier. _If this file is not present_, the population will be generated based on the buildings available.
  - **satellite.png** and **satellite.pgw** *[Optional]* : if modelers want to add a georeferenced background image (e.g. GoogleMap).

- Parameters :
The parameters of the different sub-models can all be specified, either in the GAML code of the new experiment or in their own configuration files. See how to do it on [this page](parameterize).

## Tutorial video


