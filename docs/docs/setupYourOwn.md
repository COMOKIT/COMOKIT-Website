---
layout: default
title: Setting up your own
nav_order: 3
permalink: /setupYourOwn
---

# Setting up your own simulation
{: .no_toc }


How to setup COMOKIT with your own data
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Prerequite

You'll need to have a GAMA with COMOKIT installed and running. If you don't know how to do so, please refer to the [previous documentation page](gettingStarted)

## Required Data

The model requires a minimal dataset that should be, at least, composed of:

- Demographic data : 

  - A **population.csv** file that contains individual including some basic attributes, i.e. age, gender and household Identifier 

  - Mobility and activity data : What can be done ? is it in the model (a gaml file to create activities) or can we generate them outside (a csv with given column and lines)

- Spatial data:

  - **buildings.shp** : this file should contain the buildings of the considered case. Buildings have to be understood in a wide sense, as the set of locations for activities.
    The shapefile attribute table should contain the column “type” containing the type of the building.

  - **boundary.shp**: this file should contain the boundary of the studied area

  - *[Optional]* **satellite.png** and **satellite.pgw**: if modeler wants to add a georeferenced background image (e.g. Google Map).

- Epidemiological data : One csv file should be given, containing the following parameters:

| Parameter name | Definition | Type [Range] | Default value |
|:-----:|:-----:|:-----:|:-----:|
| Transmission_human | Allowing infections from humans | Boolean | TRUE |
| Transmission_building | Allowing infections from buildings | Boolean | TRUE |
| Successful_contact_rate_human | Successful contact rate for infected humans | Real [≥0] | 0.007086298 |
| Successful_contact_rate_building | Successful contact rate for contaminated buildings | Real [≥0] | 0.007086298 |
| Reduction_asymptomatic | Reduction of the successful contact rate for asymptomatic | Real [0-1] | 0.45 |
| Proportion_asymptomatic | Proportion of asymptomatic infections | Real [0-1] | 0.3 |
| Proportion_dead_asymptomatic | Proportion of fatal symptomatic infections | Real [0-1] | 0.01 |
| Basic_viral_release | Value of viral release in the environment by an infectious individual | Real [≥0] | 3 |
| Basic_viral_decrease | Value of the viral decrease in the environment per step | Real [≥0] | 0.01375 |
| Probability_true_positive | Probability of an infected individual to be positive  | Real [0-1] | 0.89 |
| Probability_true_negative | Probability of a non-infected individual to be negative | Real [0-1] | 0.92 |
| Proportion_wearing_mask | Proportion of Individuals wearing mask | Real [0-1] | 0 |
| Reduction_wearing_mask | Reduction of the successful contact rate for Individuals wearing mask | Real [0-1] | 0.5 |
| Distribution_type_incubation | Type of the distribution for the incubation period | String [Normal, Gamma, Lognormal, Weibull] | Lognormal |
| Parameter_1_incubation | First parameter of the distribution of the incubation period | Real | 1.57 |
| Parameter_2_incubation | Second parameter of the distribution of the incubation period | Real | 0.65 |
| Distribution_type_serial_interval | Type of the distribution for the serial interval | String [Normal, Gamma, Lognormal, Weibull] | Normal |
| Parameter_1_serial_interval | First parameter of the distribution for the serial interval | Real | 3.96 |
| Parameter_2_serial_interval | Second parameter of the distribution for the serial interval | Real | 3.75 |
| Distribution_type_onset_to_recovery | Type of the distribution for the onset to recovery period | String [Normal, Gamma, Lognormal, Weibull] | Lognormal |
| Parameter_1_onset_to_recovery | First parameter of the distribution for the onset to recovery period | Real | 3.034953 |
| Parameter_2_onset_to_recovery | Second parameter of the distribution for the onset to recovery period | Real | 0.34 |

## Tutorial video

<iframe width="560" height="315" src="https://www.youtube.com/embed/sQI63mgtYi4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>