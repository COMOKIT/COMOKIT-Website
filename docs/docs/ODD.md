---
layout: default
title: Model description
nav_order: 98
permalink: /odd
---

# Short description of the COMOKIT model
{: .no_toc }

We describe in this page the COMOKIT model (version 1.0.1) using the standard O.D.D. protocol ([the full description is also available](https://comokit.org/ressources/ODD-COMOKIT_v1.0.1.pdf)).
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---


## Overview 

### Purpose

This model aims at simulating and comparing the application of COVID-19 spread mitigation policies at the scale of a closed commune, the transmission of the disease being modeled at the individual scale. Its purpose is to support deciders and researchers in answering questions such as: Is the containment of a neighborhood more effective than that of an entire village? Does closing schools decrease the transmission peaks ? How does wearing masks impact the dynamics of the epidemy ? How long should a lockdown ideally last ? What proportion of the population should be allowed to undertake activities during a lockdown ?

Several case studies are provided with the model: two Vietnamese communes of Son Loi (Vinh Phuc, Vietnam) and Thua Duc (Ben Tre, Vietnam); the small town of Castanet Tolosan (near Toulouse, France); and one abstract data sample.

Beyond these case studies, the model has been designed as a framework generic enough to be applied to any case study as long as the correct input data is provided. In particular, there is a template model ready to be re-used to start applying COMOKIT on a new set of data (see more in [setupYourOwn](setupYourOwn))

### Entities, state variables, and scales

#### Scales

The simulation model have been designed to be executed at the scale of a commune (around 10km2 and 10k inhabitants) but there is no limitation on the scale of the model except computer power to be simulated. The smallest considered spatial units are individual buildings.

The simulations are not launched from a specific starting date, but rather from the introduction of the first infected cases in the population and will run until the end of the epidemic. The simulation step is set to 1 hour. 

#### Entities

The core entity of the model is the `Individual` agents (or species): it represents individual inhabitants of the commune with their individual characteristics (age, sex, employment status) and their epidemiological status and related variables. They perform their daily activities depending on their personal agenda. This agenda is a generated set of `Activity` that can be shared by several individuals (e.g. going to a restaurant with some friends), depending on the age and family status of the `Individual` agent. `Individual` agents’ attributes include their relatives (i.e. the household), their friends , their colleagues (or classmates) and their home, working place and school `Building`. 

`Building` agents are spatial entities where the `Individual` agents can perform an `Activity`, whether this `Activity` depending on the `Building` type. Two special `Building` kinds have been defined as they have an important role in the simulation: `outside`, that represents everything outside the studied area, and `Hospital`, where sick `Individual` agents with critical symptoms can be contained and healed.

The `Individual` hourly behavior is driven by their agenda attribute that associates to some hours of the day an `Activity`. `Individuals` have preferences for activities that can be parametrized according to their age and sex : for a leisure activity, a child may prefer to go to a game center while an older person may prefer to go to a movie theater.  The `Building`  place to carry out an activity can be elicited at random (uniformly),  choosing the closest one, or following a probability as a negative function of distance and positive function of area of the targeted place.

We have also defined additional specific `Activity` species to represent the main classical kinds of `Activity`: `visiting_neighbor, working, staying_home, studying, visiting_friend`. Of course, customs activities can also be created from the generic `Activity` species.

### Process overview and scheduling

The dynamics of the model can be summarized by three main dynamics: the epidemic dynamics, the hourly activities of the `Individual` agents and the dynamics of policy adoption and application.

Considering the epidemic dynamics, there are two different pathways of infection for `Individual` agents: either through `Individual`-to-`Individual` transmission, or through persistence of the virus in the environment. 

A simulation step starts by the `Individual` agents checking whether they are infected or infect other `Individuals`. They then update their epidemic status and their individual behavior related to mask wearing. Next, they execute their daily activities (depending on `Authority` allowances). Finally, the `Authority` agent checks its current `Policy` and apply it.

## Design Concepts

### Basic principles

As far as the epidemiological dynamics is concerned, we rely on a SEIR model with an infectious state that can be presymptomatic, symptomatic or asymptomatic, with a certain degree of survivability of the virus in the environment.

The `Individual` agents’ behavior is described using an activity-based approach: people have a set of activities associated with some day hours. This agenda makes the agents move from `Building` to `Building` (due to the 1-hour step of the simulation). 

### Interaction

`Individual` agents can infect other `Individual` agents directly through contact or indirectly through building contamination: the virus can survive in the `Building` for a period of time. Interactions between `Individual` agents and the `Authority` agents occur in both directions.

### Collectives

`Individual` agents are part of several agents collectives: relatives, friends, colleagues, activity fellows. Nevertheless these collectives are not agentified with a specific behavior. The only impact is on the transmission in a same `building`. The main idea is that individuals in the same building will not have the same number of contacts with all the individuals in a (working or home) building. They thus have more chances to infect close colleagues or relatives.

## Details

### Built-in synthetic population generator 

The synthetic population of agents comprises three dimensions of agent attributes to be generated: *demographic variables*, including `age, sex`, employment status (`is_unemployed`) and households (`household_id`), *social network variables*, including the lists of `friends, colleagues or classmates`, and lastly *mobility variables* including activity timeline and corresponding activity locations (`agenda_week`). In this version of the model, only demographic variables can be initialized from an external csv file generated by an external synthetic population generator. The other variables are generated from a COMOKIT built-in generator.

For the external synthetic population generator, we choose to use the Gen* generator (that can also be coupled with the [GAMA platform](https://github.com/ANRGenstar/genstar.gamaplugin)):
>Chapuis, K., Taillandier, P., Renaud, M., & Drogoul, A. (2018). Gen*: a generic toolkit to generate spatially explicit synthetic populations. International Journal of Geographical Information Science, 32(6), 1194-1210.

### Synthetic agenda

Each agent of the model has its own set of timely organized activities, i.e. a synthetic agenda. The generation of agendas is based on demographic attributes of the agent, such as sex, age and employment status, and the specification of workdays and days off during the week.

## Submodels

### Epidemiological submodel

The epidemiological model is based on the SEIR model with an infectious state that can be presymptomatic, symptomatic or asymptomatic. Once the infectious period is over, `Individual` agents reach the Removed (R) state, representing the fact that the `Individual` has been infected, but is not infectious anymore. To represent deaths and recoveries, we decided to consider  the current clinical status of the Individual agent: when it becomes symptomatic, an `Individual` will first need hospitalisation, and then (with a given probability) ICU. If the Individual agent is not being taken to a `Hospital` before the end of its expected period needing ICU, it will be considered as dead due to lack of treatment. In the case, it went to ICU when needed, it has a probability to recover. 

The various (incubation...) periods and probabilities are `Individual`dependent and are randomly picked following various distributions.

### Daily Activities

Once weekly and daily agendas have been created at initialization, `Individual` agents have only to get, at each simulation step, the `Activity` corresponding to the current day and current hour, asks the `Authority` agent’s authorization to perform it, finds a `building` associated with the `Activity`, and moves in it. In addition, the agent will ask the `Authority` for the number of individuals it can perform the `Activity` with. 

### Institutions

The `Authority` agent is in charge of applying one or several mitigation policies on the whole case study or on some local spaces. The policies can impact the simulation in two ways. Every step, the `Authority` can proactively perform some actions encoded in the policy, e.g. conduct a given number of tests on the population. On the other hand, each `Individual` agent asks the `Authority` whether it is allowed to execute a given `Activity`. In this case, the `Authority` will make its choice based on what is allowed by its policies that are currently applied.
