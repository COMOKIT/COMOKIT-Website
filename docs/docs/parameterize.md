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
There are two different ways to set up epidemiological parameters in COMOKIT: 
- by modifying the parameters variables in Model/Parameters.gaml (setting the variable ``load_epidemiological_parameter_from_file`` to ``false``),
- by giving the path of a CSV file containing different values for the parameters (setting the variable ``epidemiological_parameters`` to the path of the file).

In both cases, a map of parameters (``map_epidemiological_parameters``, defined in ``Model/Global.gaml``) will be generated, using different ages (int) as key of the map, and the value of the parameters.

### Modifying the parameters in Model/Parameters.gaml
The first method is easier, as the parameters are already defined and just their values have to be changed. However, it lacks flexibility and heterogeneity compared to the second method.

**Note that this method is not the one used by default in COMOKIT, but the second one, providing more realistic values.**

#### Environmental contamination dynamics
The list of the epidemiological parameters presented in Model/Parameters.gaml for environmental contamination dynamics is: 
-  ``allow_transmission_building``, allowing environmental contamination dynamics, set by default to ``true``,
- ``basic_viral_decrease``, the decrease over time of the viral load in the environment, set by default to ``0.33``,
- ``basic_viral_release``, the release over time of the viral load in the environment by one infected Individual, set by default to ``3.0``,
- ``successful_contact_rate_building``, the successful contact rate for environment to human transmission derivated from the R0 and the mean infectious period, set by default to ``2.5 * 1/(14.69973*nb_step_for_one_day)``,

#### Human to human transmission dynamics
The list of the epidemiological parameters presented in Model/Parameters.gaml for human to human transmission dynamics is: 
- ``allow_transmission_human``, allowing human to human transmission dynamics, set by default to ``true``,
- ``init_all_ages_factor_contact_rate_asymptomatic``, the non-age-dependent factor of the successful contact rate for asymptomatic/presymptomatic human to human transmission, set by default to ``0.55``,
- ``init_all_ages_proportion_asymptomatic``, the non-age-dependent proportion of asymptomatic individuals, set by default to ``0.3``,
- ``init_all_ages_successful_contact_rate_human``, the non-age-dependent successful contact rate for human to human transmission derivated from the R0 and the mean infectious period, set by default to ``2.5 * 1/(14.69973)``,
-``reduction_coeff_all_buildings_individuals``, the reduction of the contact rate for individuals belonging to different households but living in the same building, set by default to ``0.05``,
- ``reduction_coeff_all_buildings_inhabitants``, the reduction of the contact rate for individuals belonging to different households but living in the same building, set by default to ``0.01``,
- ``init_all_ages_distribution_type_incubation_period_symptomatic``, the non-age-dependent distribution for the incubation period of symptomatic Individuals, set by default to ``Lognormal``,
- ``init_all_ages_parameter_1_incubation_period_symptomatic``, the first parameter for the non-age-dependent distribution for the incubation period of symptomatic Individuals, set by default to ``1.57``,
- ``init_all_ages_parameter_2_incubation_period_symptomatic``, the second parameter for the non-age-dependent distribution for the incubation period of symptomatic Individuals, set by default to ``0.65``,
- ``init_all_ages_distribution_type_incubation_period_asymptomatic``, the non-age-dependent distribution for the incubation period of asymptomatic Individuals, set by default to ``Lognormal``,
- ``init_all_ages_parameter_1_incubation_period_asymptomatic``, the first parameter for the non-age-dependent distribution for the incubation period of asymptomatic Individuals, set by default to ``1.57``,
- ``init_all_ages_parameter_2_incubation_period_asymptomatic``, the second parameter for the non-age-dependent distribution for the incubation period of asymptomatic Individuals, set by default to ``0.65``,
- ``init_all_ages_distribution_type_serial_interval``, the non-age-dependent distribution for the serial interval, set by default to ``Normal``,
- ``init_all_ages_parameter_1_serial_interval``, the first parameter for the non-age-dependent distribution for the incubation period of asymptomatic Individuals, set by default to ``3.96``,
- ``init_all_ages_parameter_2_serial_interval``, the second parameter for the non-age-dependent distribution for the incubation period of asymptomatic Individuals, set by default to ``3.75``,
- ``init_all_ages_distribution_type_infectious_period_symptomatic``, the non-age-dependent distribution for the infectious period of symptomatic Individuals, set by default to ``Lognormal``,
- ``init_all_ages_parameter_1_infectious_period_symptomatic``, the first parameter for the non-age-dependent distribution for the infectious period of symptomatic Individuals, set by default to ``3.034953``,
- ``init_all_ages_parameter_2_infectious_period_symptomatic``, the second parameter for the non-age-dependent distribution for the infectious period of symptomatic Individuals, set by default to ``0.34``,
- ``init_all_ages_distribution_type_infectious_period_asymptomatic``, the non-age-dependent distribution for the infectious period of asymptomatic Individuals, set by default to ``Lognormal``,
- ``init_all_ages_parameter_1_infectious_period_asymptomatic``, the first parameter for the non-age-dependent distribution for the infectious period of asymptomatic Individuals, set by default to ``3.034953``,
- ``init_all_ages_parameter_2_infectious_period_asymptomatic``, the second parameter for the non-age-dependent distribution for the infectious period of asymptomatic Individuals, set by default to ``0.34``.

#### Hospitalisation and severity
The list of the hospitalisation and severity related parameters presented in Model/Parameters.gaml for human to human transmission dynamics is: 
- ``init_all_ages_proportion_hospitalisation``, the non-age-dependent proportion of symptomatic Individuals that will need hospitalisation, set by default to ``0.2``,
- ``init_all_ages_distribution_type_onset_to_hospitalisation``, the non-age-dependent distribution of the time between symptom onset and hospital admission for symptomatic Individuals, set by default to ``Lognormal``,
- ``init_all_ages_parameter_1_onset_to_hospitalisation``, the first parameter of the non-age-dependent distribution of the time between symptom onset and hospital admission for symptomatic Individuals, set by default to ``3.034953``,
- ``init_all_ages_parameter_2_onset_to_hospitalisation``, the second parameter of the non-age-dependent distribution of the time between symptom onset and hospital admission for symptomatic Individuals, set by default to ``0.34``,
- ``init_all_ages_proportion_icu``, the non-age-dependent proportion of hospitalised Individuals that will need to go in ICU, set by default to ``0.1``,
- ``init_all_ages_distribution_type_hospitalisation_to_ICU``, the non-age-dependent distribution of the time between hospitalisation and ICU admission for hospitalised Individuals, set by default to ``Lognormal``,
- ``init_all_ages_parameter_1_hospitalisation_to_ICU``, the first parameter of the non-age-dependent distribution of the time between hospitalisation and ICU admission for hospitalised Individuals, set by default to ``3.034953``,
- ``init_all_ages_parameter_2_hospitalisation_to_ICU``, the second parameter of the non-age-dependent distribution of the time between hospitalisation and ICU admission for hospitalised Individuals, set by default to ``0.34``,
- ``init_all_ages_distribution_type_stay_ICU``, the non-age-dependent distribution of the duration of stay in ICU for Individuals, set by default to ``Lognormal``,
- ``init_all_ages_parameter_1_stay_ICU``, the first parameter of the non-age-dependent distribution of the duration of stay in ICU for Individuals, set by default to ``3.034953``,
- ``init_all_ages_parameter_2_stay_ICU``, the second parameter of the non-age-dependent distribution of the duration of stay in ICU for Individuals, set by default to ``0.34``,
- ``init_all_ages_proportion_dead_symptomatic``, the non-age-dependent proportion of symptomatic individuals that will die even if treated, set by default to ``0.01``,

#### Testing and mask wearing
The list of the test and mask related parameters presented in Model/Parameters.gaml for human to human transmission dynamics is: 
- ``init_all_ages_probability_true_negative``, the non-age-dependent probability of being tested positive when infected, set by default to ``0.92``,
- ``init_all_ages_probability_true_positive``, the non-age-dependent probability of being tested positive when infected, set by default to ``0.89``,
- ``init_all_ages_proportion_wearing_mask``, the non-age-dependent proportion of Individuals wearing mask, set by default to ``0.0``,
- ``init_all_ages_factor_contact_rate_wearing_mask``, the non-age-dependent factor of successful transmission for an infectious individual wearing a mask, set by default to ``0.5``,


### Modifying the parameters in the CSV file
 In the CSV file, it is possible to define multiple values for the same parameter taking into account the age of the individuals. In addition, it is possible to not just provide a fixed value, but also a distribution in order to generate different values for each Individual (among Weibull, Gamma, Uniform, Normal and Lognormal distributions). In the case of providing a CSV file to set the parameters, it is still possible to force parameter values (for one experiment, for instance) by using the ``force_parameters`` map, expecting the string ID of a parameters (defined in ``Model/Constants.gaml``) and a given value. 
Particular attention should be given to the names of the parameters provided in the CSV file, as they must be exactly the same as the string ID of the parameters. In order to define a parameter as age-depedent, multiple rows in the CSV file must begin with the same parameter string ID, and different age values. The age category will be defined with the lower bound equals to the value of the column age for the given row, and the upper bound the value of the column age for the next row with the same parameter string ID (if there are none, there will be no upper bound, including every Individuals having at least an age equals to the lower bound). The column detail in the CSV is expecting either the string ``FIXED`` (for a parameter not following a distribution), or one of the string ID of the distributions (``Weibull``, ``Gamma``, ``Normal``, ``Lognormal``, ``Uniform``). Parameter_1 is expecting the value of the parameter (if ``FIXED``) or the first parameter of the gama function for the given distribution. Parameter_2 is used only if Detail is a distribution, and provides the second parameter of the gama function for the given distribution.

All the parameters can have different values for given age categories but: 
- ``Transmission_human`` (corresponding to ``allow_transmission_human`` in ``Model/Parameters.gaml``), allowing human to human transmission dynamics,
- ``Transmission_building`` (corresponding to ``allow_transmission_building`` in ``Model/Parameters.gaml``), allowing environmental contamination dynamics,
- ``Successful_contact_rate_building`` (corresponding to ``successful_contact_rate_building`` in ``Model/Parameters.gaml``), the transmission building to human occuring due to environmental contamination, 
- ``Basic_viral_decrease`` (corresponding to ``basic_viral_decrease`` in ``Model/Parameters.gaml``), the decrease over time in viral load in the environment,
can't be age-dependent for obvious reasons. 

The default values for the different parameters are stored in the file ``Parameters/Epidemiological Parameters.csv``.



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

## To link building types and activities

Synthetic agenda of agents provides time use according to a sequence of activites to be carried out in buildings. In order to choose appropriate building corresponding to their activities, it is necessary to determine case study related building types and to attached these types to an activity.  

### Building types
COMOKIT provides built-in types of buildings, most of which have been taken from the [OSM nomenclature](https://wiki.openstreetmap.org/wiki/Key:building). They are stored in the ``Paramaeters/Building type per activity type.csv`` file, with first column standing for activity type, and following ones to corresponding building types. For example, default provided type of building for ``staying_at_home`` activity are: ``" "`` (empty string), ``yes``, ``house``, ``manor``, ``apartments``, ``caravan``, ``hostel``, ``home`` and ``Tent Shelter``. For any missing type, i.e. case study ``buildings.shp`` file where home place type is not in the previous list, you may have to add in a new column the corresponding type name. Hence, COMOKIT will be able to link activity types to custom building types.

### Building file
The building file is used to define the agent preferences for building types according to age and sex. The higher the weigths are the higher individual agent will tends to carried out activities within this particular type of building. For example, agents can perform a leisure activity in several types of buildings, including cinema, karaoke, coffeshops and many more defined in ``Building per type activity type.csv`` (see [Activity to building](#Buildin-types) section). In that respect, the weights attached to building type will determine the corresponding probability to carry out a leisure activity in a particular building. Any missing building type will be assigned a weight equal to ``1.0``.

As for the activity file, the building file should be created and placed in a case study folder, and named ``Building type weights.csv``. The table below show a snippet example of a file content: 

| Age min | Age max | sex | playground | park | cinema | place_of_worship |
|---------|---------|-----|------------|------|--------|------------------|
| 0       | 10      | 0   | 1.0        | 1.0  | 0.5    | 0.5              |
| 0       | 10      | 1   | 1.0        | 1.0  | 0.5    | 0.5              |
| 11      | 18      | 0   | 0.2        | 0.5  | 1.0    | 0.5              |
| 11      | 18      | 1   | 0.2        | 0.5  | 1.0    | 0.5              |
| 19      | 60      | 0   | 1.0        | 1.0  | 1.0    | 1.0              |
| 19      | 60      | 1   | 1.0        | 1.0  | 1.0    | 2.0              |
| 61      | 120     | 0   | 2.0        | 2.0  | 0.5    | 1.0              |
| 61      | 120     | 1   | 2.0        | 2.0  | 0.5    | 2.0              |

## Redefining parameter values

As a general advice, parameters in ``Parameters.gaml`` and variables (e.g. in ``Global.gaml``) of COMOKIT should be redefined in user models: it is good practice to redefine them in a ``global`` section of a user created GAML file. For example, to redefine the number of infected and recovered individuals at the beginning of a simulation, open or create a new GAML file, import all required files from COMOKIT and assign new values as follow:
```
global {
  int num_infected_init <- 10;
  int num_recovered_init <- 500; 
}
```
As a general guideline, do not change the values of parameters directly in the COMOKIT code, but rather in your own model (that imports COMOKIT). This advice is not mandatory at all, and modifying your local version of COMOKIT is functional. However, for the sake of clarity, it is recommended to redefine the parameters/variables of interest for you, in a model specific user created file.
