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

## Synthetical population

As mentioned in the [ODD](link to the ODD), COMOKIT makes it possible to generate a synthetic population of agent following two path: from a csv file where each line correspond to an individual or using the built-in generator. In this paragraph we details how they can be parametrized (for a complete description of the process, please refer to the ODD). In the following sub-section we review how to customize the [built-in generator](#Built-in-generator-parametrization) and how to harmonize [file based synthetic records](#File-based-data-harmonization)

### Built-in generator parametrization

The default generator provided with COMOKIT makes use of a configuration files in order to define key variables of the algorithm. In order to define them according to a case study, it should be created and placed in the specific case study folder, following the convention name ``Population parameter.csv``, with first column corresponding to the parameter name and second column the provided value. The list below details all possible parameters to be define within this file with the default value when omitted:

 - ``male_ratio`` : the probability to be a male (``1 - male_ratio`` gives the probability to be a female). Default is ``21/41``
 - ``proba_active_family`` : the probability to create a two or more person household (``1 - proba_active_family`` being the probability to create a lone individual household). Default is ``0.95``
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

In order to use micro-data to initialize the synthetic population of agent in COMOKIT, users should provide attribute name and value matches for ``age``, ``sex``, ``is_unemployed`` and ``household_id`` ``Individual`` attributes. For the [Version 1.0](https://comokit.org/docs/version1), these information must be given in Gaml language within user's model. We listed below which variables must be overwritten to harmonize your micro-data with COMOKIT:

- ``age`` : assigne the name of micro-data age variable to ``age_var`` (i.e. ``age_var <- "age_var_name_in_csv"``) and the mapping of values in ``age_map`` (e.g. ``age_map <- ["0-14"::[0,14],"15-45"::[15,45],"46+"::[46,120]]``)
- ``sex`` : assigne the name of micro-data sex variable to ``sex_var`` (i.e. ``sex_var <- "sex_var_name_in_csv"``) and the mapping of values in ``sex_map`` (e.g. ``sex_map <- ["homme"::0,"femme"::1]``)
- ``is_unemployed`` : assigne the name of micro-data employement status to ``unemployed_var`` (i.e. ``unemployed_var <- "employement_var_name_in_csv"``) and the mapping of values in ``unemployed_map`` (e.g. ``unemployed_map <- ["active"::false,"inactive"::true,"unemployed"::true]``)
- ``household_id`` : assigne the name of micro-data household identifier to ``householdID`` (i.e. ``householdID <- "household_id_name_in_csv"``)

Each one has a built-in method to get a default value when data is missing or missencoding. Age will be uniformly drawn in ``[0,max_age]`` (with ``max_age`` a variable of COMOKIT that can be found in ``Parameters.gaml``), Gender choosen according to a probability of 0.512 (ratio of 105 male for 100 female) and an unemployed rate of 0.03 (i.e. same rate as in the built-in generator). When no household identifier is provided in the micro-data, COMOKIT will built household as the built-in generator does, except it selected relevant individuals from the sample rather than creating them.

## Synthetical agenda

## Activities

## Redefining parameter value

As a general advice, parameters in ``Parameters.gaml`` and variables (e.g. in ``Global.gaml``) of COMOKIT should be redefined in user models: it is good practice to redefine them in a ``global`` section of a user created gaml file. For examples, to redefine the number of infected and recovered individuals at the beginning of a simulation, open or create a new gaml file, import all required from COMOKIT and assign new values as follow:
```
global {
  int num_infected_init <- 10;
  int num_recovered_init <- 500; 
}
```
As a general guideline, do not change the values of parameters directly in the COMOKIT code, but rather in your own model that makes use of COMOKIT.
