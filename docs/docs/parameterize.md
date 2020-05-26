---
layout: default
title: Parameterizing simulations
nav_order: 3
description: "Setting up your COMOKIT Model"
permalink: /parameterize
---

# Parameterizing simulations 
{: .no_toc }

<!--
Text header
{: .fs-6 .fw-300 }
-->

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Epidemiology

## Synthetic population generation

As mentioned in its [ODD description](https://comokit.org/ressources/ODD-COMOKIT_v1.pdf), COMOKIT proposes two ways to generate a synthetic population of agents: either from a csv file where each line corresponds to an individual or using a built-in generator. This paragraph details how both can be parameterized. The following sub-section shows how to customize the [built-in generator](#Built-in-generator-parametrization) and how to harmonize [file based synthetic records](#File-based-data-harmonization)

### Built-in generator parameterization

The default generator provided with COMOKIT makes use of a configuration file in order to define key variables of the algorithm. In order to define them according to a case study, it should be created and placed in the case study folder, and  named `Population parameter.csv`, with a first column corresponding to the parameter name and a second column the provided value. The list below details all the parameters that can be defined in this file with their default value when they are omitted:

 - ``male_ratio`` : the probability to be a male (``1 - male_ratio`` gives the probability to be a female). Default is ``21/41``
 - ``proba_active_family`` : the probability to create a two or more persons household (``1 - proba_active_family`` being the probability to create a lone individual household). Default is ``0.95``
 - ``number_children_mean`` : the mean (expected value) number of children per household. Default is ``2.0``
 - ``number_children_std`` : the standard deviation (variance) to determine the number of children per household. Default is ``0.5``
 - ``number_children_max`` : the maximum number of children per household. Default is ``3``
 - ``proba_grandfather`` : the probability to include the grandfather in the household. Default is ``0.2``
 - ``proba_grandmother`` : the probability to include the grandmother in the household. Default is ``0.3``
 - ``retirement_age`` : the age threshold for retirement. Default is ``55``
 - ``max_age`` : the maximum age an agent can have at initialization. Default is ``100``
 - ``nb_friends_mean`` : the mean (expected value of a Gaussian) number of friends per individual agent. Default is ``5.0``
 - ``nb_friends_std`` : the standard deviation (variance of a Gaussian) to determine the number of friends per individual. Default is ``3.0``
 - ``nb_classmates_mean`` : mean number of classmates with which an Individual will have close contact. Default is ``10.0``
 - ``nb_classmates_std`` : stand deviation of the number of classmates with which an Individual will have close contact. Default is ``5.0``
 - ``nb_work_colleagues_mean`` mean number of work colleagures with which an Individual will have close contact. Default is ``5.0``
 - ``nb_work_colleagues_std`` : stand deviation of the number of work colleagures with which an Individual will have close contact. Default is ``3.0``
 - ``proba_work_at_home`` : the probability to do remote work. Default is ``0.05``
 - ``proba_unemployed_M`` : the probability for a male individual agent to be unemployed. Default is ``0.03``
 - ``proba_unemployed_F`` : the probability for a female individual agent to be unemployed. Default is ``0.03``

### File based data harmonization

In order to use microdata to initialize the synthetic population of agents in COMOKIT, users should provide attribute names and values for ``age``, ``sex``, ``is_unemployed`` and ``household_id`` ``Individual`` attributes. In [Version 1.0](https://comokit.org/docs/version1) of COMOKIT, these information must be provided directly in the `global` section in GAML. Below are listed the variables that must be overwritten to harmonize the micro-data with COMOKIT:

- ``age`` : assigns the name of micro-data age variable to ``age_var`` (i.e. ``age_var <- "age_var_name_in_csv"``) and the mapping of values in ``age_map`` (e.g. ``age_map <- ["0-14"::[0,14],"15-45"::[15,45],"46+"::[46,120]]``)
- ``sex`` : assigns the name of micro-data sex variable to ``sex_var`` (i.e. ``sex_var <- "sex_var_name_in_csv"``) and the mapping of values in ``sex_map`` (e.g. ``sex_map <- ["man"::0,"woman"::1]``)
- ``is_unemployed`` : assigns the name of micro-data employement status to ``unemployed_var`` (i.e. ``unemployed_var <- "employement_var_name_in_csv"``) and the mapping of values in ``unemployed_map`` (e.g. ``unemployed_map <- ["active"::false,"inactive"::true,"unemployed"::true]``)
- ``household_id`` : assigns the name of micro-data household identifier to ``householdID`` (i.e. ``householdID <- "household_id_name_in_csv"``)

Each one has a built-in method to get a default value when data is missing or missencoding. The age will be uniformly drawn in ``[0,max_age]`` (with ``max_age`` being a variable of COMOKIT that can be found in ``Parameters.gaml``), Gender chosen according to a probability of 0.512 (ratio of 105 males for 100 females) and an unemployed rate of 0.03 (i.e. same rate as in the built-in generator). When no household identifier is provided in the micro-data, COMOKIT builds households like the built-in generator does, except it selects relevant individuals from the sample rather than creating them.

## Synthetic agenda


The synthetic agenda generator provided with COMOKIT makes use of two files: a configuration file and an activity file.

### Synthetic agenda configuration file
The configuration file is used to define the key variables of the algorithm. In order to define them according to a case study, it should be created and placed in the case study folder, and  named `Agenda parameter.csv`, with a first column corresponding to the parameter name and a second column the provided value. The list below details all the parameters that can be defined in this file with their default value when they are omitted:

 
 - ``non_working_days`` : List of non working days (1: Monday, 7: Sunday). Default is ``[7]``
 - ``work_hours_begin_min`` : the minimal value for the beginning working hour (between 0 and 23). Default is ``6``
 - ``work_hours_begin_max`` : the maximal value for the beginning working hour (between 0 and 23). Default is ``10``
 - ``work_hours_end_min`` : the minimal value for the ending working hour (between 0 and 23). Default is ``15``
 - ``work_hours_end_max`` : the maximal value for the ending working hour (between 0 and 23). Default is ``18``
 - ``school_hours_begin_min`` : the minimal value for the beginning school hour (between 0 and 23). Default is ``7``
 - ``school_hours_begin_max`` : the maximal value for the beginning school hour (between 0 and 23). Default is ``9``
 - ``school_hours_end_min`` : the minimal value for the ending school hour (between 0 and 23). Default is ``15``
 - ``school_hours_end_max`` : the maximal value for the ending school hour (between 0 and 23). Default is ``18``
 - ``first_act_hour_non_working_min`` : For non working day (or people who are not working), minimal hour for the beginning of the first activity (between 0 and 23). Default is ``7``
 - ``first_act_hour_non_working_min`` : For non working day (or people who are not working), maximal hour for the beginning of the first activity (between 0 and 23). Default is ``10``
 - ``lunch_hours_min`` : the minimal value for the beginning of the lunch time (between 0 and 23). Default is ``11``
 - ``lunch_hours_max`` : the maximal value for the beginning of the lunch time (between 0 and 23). Default is ``13``
 - ``max_duration_lunch`` : the maximal duration (in hours) of the lunch time. Default is ``2``
 - ``max_duration_default`` : the maximal duration (in hours) of other activities. Default is ``3``
 - ``min_age_for_evening_act`` : the minimal age of individual to have an activity after school. Default is ``13``
 - ``nb_activity_fellows_mean`` : the mean number of fellows per activity. Default is ``3.0``
 - ``nb_activity_fellows_std`` : the standard deviation of the number of fellows per activity. Default is ``2.0``
 - ``max_num_activity_for_non_working_day`` : the maximal number of activities for non working day. Default is ``4``
 - ``max_num_activity_for_unemployed`` : the maximal number of activities per day for unemployed individual. Default is ``3``
 - ``max_num_activity_for_old_people`` : the maximal number of activities per day for retired individual. Default is ``3``
 - ``proba_activity_evening`` : the probability for people to have an activity after work. Default is ``0.7``
 - ``proba_lunch_outside_workplace`` : the probability to have lunch outside the working place (home or restaurant). Default is ``0.5``
 - ``proba_lunch_at_home`` : if lunch taken outside the working place, the probability of having lunch at home. Default is ``0.5``
 - ``proba_work_outside`` : the probabilty for an individual to work outside the considered area. Default is ``0.0``
 - ``proba_go_outside`` : the probabilty for an individual to do an activity outside the considered area. Default is ``0.0``
 - ``building_neighbors_dist`` : the maximal distance (in meter) of the considered neigbhorhood for the "visit to neighbors" activity. Default is ``500.0``



### Activity file
The activity file is used to define, according to the Individual’s age and the sex category, the weights of the different types of activity (the higher the weight, the higher the chance to carried out this activity).
In order to define it according to a case study, it should be created and placed in the case study folder, and named `Activity type weights.csv`.The table below shows an example of file

| Age min | Age max | sex | visiting neighbor | visiting friend | eating | shopping | leisure | outside activity | sport | other activity |
|---------|---------|-----|-------------------|-----------------|--------|----------|---------|------------------|-------|----------------|
| 0       | 10      | 0   | 1.0               | 1.0             | 0.5    | 0.5      | 1.0     | 2.0              | 1.0   | 0.1            |
| 0       | 10      | 1   | 1.0               | 1.0             | 0.5    | 0.5      | 1.0     | 2.0              | 1.0   | 0.1            |
| 11      | 18      | 0   | 0.2               | 0.5             | 1.0    | 0.5      | 2.0     | 2.0              | 1.0   | 0.1            |
| 11      | 18      | 1   | 0.2               | 0.5             | 1.0    | 0.5      | 2.0     | 2.0              | 1.0   | 0.1            |
| 19      | 60      | 0   | 1.0               | 1.0             | 1.0    | 1.0      | 2.0     | 1.0              | 1.0   | 1.0            |
| 19      | 60      | 1   | 1.0               | 1.0             | 1.0    | 2.0      | 2.0     | 1.0              | 1.0   | 1.0            |
| 61      | 120     | 0   | 2.0               | 2.0             | 0.5    | 1.0      | 0.5     | 0.5              | 0.2   | 2.0            |
| 61      | 120     | 1   | 2.0               | 2.0             | 0.5    | 2.0      | 0.5     | 0.5              | 0.1   | 2.0            |

## Redefining parameter values

As a general advice, parameters in ``Parameters.gaml`` and variables (e.g. in ``Global.gaml``) of COMOKIT should be redefined in user models: it is good practice to redefine them in a ``global`` section of a user created GAML file. For example, to redefine the number of infected and recovered individuals at the beginning of a simulation, open or create a new GAML file, import all required files from COMOKIT and assign new values as follow:
```
global {
  int num_infected_init <- 10;
  int num_recovered_init <- 500; 
}
```
As a general guideline, do not change the values of parameters directly in the COMOKIT code, but rather in your own model (that imports COMOKIT).
