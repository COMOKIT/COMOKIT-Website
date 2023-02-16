---
layout: default
title: Model description
nav_order: 10
permalink: /odd
---
# Short description of the COMOKIT tookit
COMOKIT proposes 3 models based on a common foundation, each adapted to a different scale of analysis: the Meso model corresponds to the historical model of COMOKIT and is adapted to simulations at the scale of a neighborhood or a small city. The Micro model allows to represent explicitly the movements of people and is adapted to simulations at the scale of a building or a small set of buildings. Finally, COMOKIT macro, which does not propose an individual representation of people, is adapted to perform large-scale simulations.

{: .no_toc .text-delta }

---

# Description of the COMOKIT Meso model
{: .no_toc }
We describe in this section the COMOKIT Meso model (version 2.0) using the standard O.D.D. protocol ([the full description is also available](https://comokit.org/ressources/ODD-COMOKIT_Meso_v2.pdf)).


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

---

# Description of the COMOKIT Micro model
{: .no_toc }
We describe in this section the COMOKIT Micro model (version 2.0) using the standard O.D.D. protocol ([the full description is also available](https://comokit.org/ressources/ODD-COMOKIT_Micro_v2.pdf)).

## Overview 

### Purpose

This model aims at simulating and comparing the application of COVID-19 spread mitigation policies at the scale of a building or a small set of buildings, the transmission of the disease being modeled at the individual scale. Its purpose is to support deciders and researchers in answering questions such as: Is the containment of some rooms more effective than that of an entire floor? What is the impact of wearing masks on the dynamics of the epidemic? What should be the maximum density to limit spread? What proportion of the population should be allowed to undertake activities during a lockdown?

Two case studies are provided with the model: one concerning a classic office with a second building representing the office restaurant; one concerning the hospital of Danang.

### Entities, state variables, and scales

#### Scales

The simulations are executed at the scale of a set of buildings. The smallest considered spatial units are individual rooms.

The simulations are not launched from a specific starting date, but rather from the introduction of the first infected cases in the population and will run until the end of the epidemic. The simulation step is set to 1 minute. 


#### Entities

The model is designed to simulate the COVID-19 spread at the individual scale. As a consequence, the core entity of the model is the `Individual` kind of agents (or species): it represents individual users of the buildings with their individual characteristics (age, sex, employment status) and their epidemiological status, whether they have been tested, and other epidemiological individual-dependent values (e.g. latent_time, infectious_time … c.f. the epidemiological submodel description for more details). They perform their daily activities (including going to their office, going to the restaurant, going to the meeting room…) depending on their personal agenda. This agenda is a generated set of Activity.

`Room` agents are spatial entities where the `Individual` agents can perform an `Activity`. A `Room` has one or several `RoomEntry` agents and several `Wall` agents. It is located at a specific floor of a `Building` agent. A specific type of `Room` is `Elevator`, allowing `Individual` agents to pass from one floor to another one. In addition to `Room` agents, a `Building` agent has one or several `BuildingEntry` agents. The global environment is characterized by `Building` agents, but also by one or several `AreaEntry` agents and by `PedestrianPath` agents representing the path that `Individual` agents can follow to move.

The `Individual` agent’s behavior is driven by their agenda attribute that associates to some date an `Activity`. An `Activity` is mainly a way to choose the spatial unit(s) in which the `Individual` agents have to be located or to move to at each simulation step. the last type of spatial entity are the `UnitCell` agents, which allow to take into account the environmental contamination 

We have also defined additional specific `Activity` species to represent the main classical kinds of `Activity`: `ActivityLeaveArea`, `ActivityGotoOffice`, `ActivityGotoRestaurant`, `ActivityGotoRoom`. Of course, customs activities can also be created from the generic `Activity` species.


### Process overview and scheduling

The model simulates the spread of the COVID-19 in a population at the individual level. The dynamics of the model can be summarized by two main dynamics: the epidemic dynamics and the activities of the `Individual` agents, following their agenda.

There are three different pathways of infection for `Individual` agents: either through Individual-to-Individual transmission, through persistence of the virus in the air, and through persistence of the virus on the physical objects. When an infectious Individual is located in a building, it can release a virus load on the unit cell it is located in, which can survive several hours. In addition, it can release a virus load in the room it is located in. Individuals who will come to this unit cell/room can thus become infected by the viral load present in the unit cell/room itself. As soon as an `Individual` is infected, its epidemic status will be described by a set of states and transitions (given probabilities taken from the up-to-date COVID-19 literature).

A simulation step starts by the evolution of the viral load in the unit cells and in the rooms (it decreases over time, before disappearing). Then the `Individual` agents behave. They first evaluate whether they are infected or infect other `Individual` agents or release virus load in their current unit cell/room. They then update their epidemic status (given the model detailed in the Sub-model Section) and their individual behavior related to mask wearing. Finally they execute their activities: they find the activity corresponding to the current time, and act in accordance. 


## Design Concepts

### Basic principles

As far as the epidemiological dynamics is concerned, we rely on much scientific evidence that the disease could be represented by a SEIR model with an infectious state that can be presymptomatic, symptomatic or asymptomatic, with a certain degree of survivability of the virus in the environment and the possibility of people being infected by it.

The `Individual` agents’ behavior is described using an activity-based approach: people have a set of activities associated with some corresponding time. This agenda makes the agents move from room to room (and eventually from building to building) and enter/leave the simulated area. 


### Interaction

`Individual` agents can infect other `Individual` agents directly through contact or indirectly through room and/or unit cell contamination: Infectious `Individual` agents can release a viral load in a unit cell and/or in a room agent and, as the virus can survive in the `Building` for a period of time, a unit cell and a room agent with a viral load will possibly infect the `Individual` agents located in it, following the assumption that contaminated surfaces such as doorknobs, tables, on which the virus can survive, are possible transmission pathways. 


## Details

### Initialization 
In order to keep the model as generic as possible, many parameters and initial values are stored in case-dependent external files. Two parameter files for epidemiological model and activity types links to building types are stored in a general purpose parameter folder. In order to use them in a custom version of COMOKIT, users should either redefine them or give the path to this folder relative to the new project.

## Submodels

### Epidemiological submodel

The epidemiological model is based on the SEIR model with an infectious state that can be presymptomatic, symptomatic or asymptomatic. Once the infectious period is over, `Individual` agents reach the Removed (R) state, representing the fact that the `Individual` has been infected, but is not infectious anymore. To represent deaths and recoveries, we decided to consider  the current clinical status of the Individual agent: when it becomes symptomatic, an `Individual` will first need hospitalisation, and then (with a given probability) ICU. If the Individual agent is not being taken to a `Hospital` before the end of its expected period needing ICU, it will be considered as dead due to lack of treatment. In the case, it went to ICU when needed, it has a probability to recover. 

The various (incubation...) periods and probabilities are `Individual`dependent and are randomly picked following various distributions.



---

# Description of the COMOKIT Meso model
{: .no_toc }
We describe in this section the COMOKIT Macro model (version 2.0) using the standard O.D.D. protocol ([the full description is also available](https://comokit.org/ressources/ODD-COMOKIT_Macro_v2.pdf)).



## Overview 

### Purpose

This model aims at simulating and comparing the application of COVID-19 spread mitigation policies at the scale of a big city or a country, the transmission of the disease being modeled at the scale of individual groups. Its purpose is to support decision makers and researchers in answering questions such as: Is the containment of a neighborhood more effective than that of an entire city? Does closing schools decrease the transmission peaks ? How does wearing masks impact the dynamics of the epidemic ? How long should a lockdown ideally last ? What proportion of the population should be allowed to undertake activities during a lockdown ?

One case study is provided with the model: the province (Région) of Alpes-Maritimes in France. 


### Entities, state variables, and scales

#### Scales

The model has been designed to be adapted to any scale and in particular to city and country scales. The spatial units considered can represent an individual building, a neighborhood, a city, a region or even a country.

The simulations are not launched from a specific starting date, but rather from the introduction of the first infected cases in the population and will run until the end of the epidemic. The simulation step is by default set to 1 hour (but it is possible to take into account a less fine time step). As a consequence, movements from one activity place to another one are not simulated: groups of individuals are always located in an activity place. The underlying assumption is that no infection cannot occur during the travel time.


#### Entities

The model is designed to simulate the COVID-19 spread at the individual group scale. As a consequence, the core entity of the model is `Group` type of agents (or species): it represents a homogenous group of individual inhabitants that share similar characteristics with respect to the disease and governance response (incubation time, likelihood of hospitalization, likelihood of wearing a mask, likelihood of following restrictions…). A Group allows to know for each epidemiological status (susceptible, latent, pre-symptomatic, symptomatic, asymptomatic…), the number of individuals in the group with that status. To take into account the temporal evolution of the disease, the number of individuals in each status is not kept as a simple integer, but as a table, each cell of the table corresponds to one day, e.g. the integer in the second cell of the table corresponding to the latent status corresponds to the number of individuals in the latent status for 2 days.

Another important type of agent is `Compartment`, which is an encapsulation of a Group, which represents a group of inhabitants living in the same Spatial_unit and which shares the same agenda. The agenda describes, depending on the day of the week and the time of day, the number of people in the `Compartment` who will go to each `Spatial_unit`, to perform this or that type of activity in the different types of buildings.

`Spatial_unit` agents are spatial entities where the individuals can perform an activity. They are characterized by a set of `Compartment` agents representing the inhabitants of the area, by a set of building types and for each one by the area that it represents, and finally by a set of `Group` agents representing at the current time step the individuals that are located in the area for each type of building.

As our main goal is to simulate and compare the application of various mitigation and control policies, a specific focus is made on policies that modify the population behavior to reduce contacts and thus infection between people. As a consequence, the possibility for individuals of `Compartment` agents to carry out an activity in a given `Spatial_unit` and building type is constrained by the allowance of the `Authority` agent. This agent manages the various `Policy` that are adopted. When a `Compartment` agent asks it for authorization to perform an activity, the `Authority` asks all the policies it has adopted the allowance rate for the `Compartment` to do the given `Activity`. Examples of `Policy` include total containment, close the schools, close the work spaces… These policies can be limited to a given area (using `SpatialPolicy`) or be more or less tolerant (e.g. containment can be for every body or for every body but some people, or some rate of the population, using `PartialPolicy`).


### Process overview and scheduling
The dynamics of the model can thus be summarized by four main dynamics: the epidemic status updating of `Compartment` agents, the activities of the Compartment agents,  the disease spreading, and the dynamics of policy adoption and application.

At the beginning of each new day, the epidemiological status of the group of each Compartment agent is updated. More precisely, for each epidemiological status, the number of individuals in each cell will be transferred to the next cell, corresponding to the next day. For the number of individuals in the last cell, transition rates to new statuses are used to know to which status these individuals will be transferred. 

The most important dynamic, which is triggered at each simulation step, is the movement of individuals to conduct their activity. More precisely, each Compartment agent will calculate according to its agenda and current policies the number of individuals who will go to each `Spatial_unit` agent to conduct their activity in a given type of building. This number will then be managed as a group agent located in the target `Spatial_unit` agent and linked to a building type. The set of these groups will then allow to calculate the number of susceptible individuals that will be infected for each `Compartment` agent.

Finally, the `Authority` agent checks its current `Policy` and tries to apply it (e.g. executing a test campaign for example).


## Design Concepts

### Basic principles

As far as the epidemiological dynamics is concerned, we rely on much scientific evidence that the disease could be represented by a SEIR model with an infectious state that can be presymptomatic, symptomatic or asymptomatic, with a certain degree of survivability of the virus in the environment and the possibility of people being infected by it.

The individual group agents’ behavior is described using an activity-based approach: people have a set of activities associated with some day hours. This agenda makes the individuals in the group jump between spatial units and types of buildings. 


### Interaction

The first type of interaction is the dynamics of contamination. `Group` agents in the same spatial unit and in the same types of buildings will contaminate each other. 
Interactions between Compartment agents and the `Authority` agents occur in both directions: Compartment agents ask the `Authority`’s authorization to execute a given `Activity` and reversely the `Authority` agents can apply a `Policy` to check the epidemic state of the individuals inside the `Compartment` agents.


## Details

### Initialization

In order to keep the model as generic as possible, many parameters and initial values are stored in case-dependent external files. A parameter file for the epidemiological model is stored in a general purpose parameter folder. In order to use it in a custom version of COMOKIT, users should either redefine them or give the path to this folder relative to the new project (for example, see Template Projects in COMOKIT). 

## Submodels

### Epidemiological submodel

The epidemiological model is based on the SEIR model with an infectious state that can be presymptomatic, symptomatic or asymptomatic. Once the infectious period is over, `Individual` agents reach the Removed (R) state, representing the fact that the `Individual` has been infected, but is not infectious anymore. To represent deaths and recoveries, we decided to consider  the current clinical status of the Individual agent: when it becomes symptomatic, an `Individual` will first need hospitalisation, and then (with a given probability) ICU. If the Individual agent is not being taken to a `Hospital` before the end of its expected period needing ICU, it will be considered as dead due to lack of treatment. In the case, it went to ICU when needed, it has a probability to recover. 

The various (incubation...) periods and probabilities are `Individual`dependent and are randomly picked following various distributions.


### Institutions

The `Authority` agent is in charge of applying one or several mitigation policies on the whole case study or on some local spaces. The policies can impact the simulation in two ways. Every step, the `Authority` can proactively perform some actions encoded in the policy, e.g. conduct a given number of tests on the population. On the other hand, each `Individual` agent asks the `Authority` whether it is allowed to execute a given `Activity`. In this case, the `Authority` will make its choice based on what is allowed by its policies that are currently applied.
