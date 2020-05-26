# Short O.D.D. description of the COMOKIT model

We describe in this document the COMOKIT model using the standard O.D.D. protocol in its first review version.

## Overview 
### Purpose

This model aims at simulating and comparing the application of COVID-19 spread mitigation policies at the scale of a closed commune, the transmission of the disease being modeled at the individual scale. Its purpose is to support deciders and researchers in answering questions such as: Is the containment of a neighborhood more effective than that of an entire village? Does closing schools decrease the transmission peaks ? How does wearing masks impact the dynamics of the epidemy ? How long should a lockdown ideally last ? What proportion of the population should be allowed to undertake activities during a lockdown ?

Several case studies are provided with the model: two Vietnamese communes of Son Loi (Vinh Phuc, Vietnam) and Thua Duc (Ben Tre, Vietnam); the small town of Castanet Tolosan (near Toulouse, France); and one abstract data sample.

Beyond these case studies, the model has been designed as a framework generic enough to be applied to any case study as long as the correct input data is provided. In particular, there is a template model ready to be re-used to start applying COMOKIT on a new set of data (see more in [link to the A to Z])

### Entities, state variables, and scales
#### Scales
The core entity of the model is the `Individual` agents (or species): it represents individual inhabitants of the commune with their individual characteristics (age, sex, employment status) and their epidemiological status and related variables. They perform their daily activities depending on their personal agenda. This agenda is a generated set of `Activity` that can be shared by several individuals (e.g. going to a restaurant with some friends), depending on the age and family status of the `Individual` agent. `Individual` agents’ attributes include their relatives (i.e. the household), their friends , their colleagues (or classmates) and their home, working place and school `Building`. 

`Building` agents are spatial entities where the `Individual` agents can perform an `Activity`, whether this `Activity` depending on the `Building` type. Two special `Building` kinds have been defined as they have an important role in the simulation: `outside`, that represents everything outside the studied area, and `Hospital`, where sick `Individual` agents with critical symptoms can be contained and healed.

The `Individual` hourly behavior is driven by their agenda attribute that associates to some hours of the day an `Activity`. `Individuals` have preferences for activities that can be parametrized according to their age and sex : for a leisure activity, a child may prefer to go to a game center while an older person may prefer to go to a movie theater.  The `Building`  place to carry out an activity can be elicited at random (uniformly),  choosing the closest one, or following a probability as a negative function of distance and positive function of area of the targeted place.

We have also defined additional specific `Activity` species to represent the main classical kinds of `Activity`: `visiting_neighbor, working, staying_home, studying, visiting_friend`. Of course, customs activities can also be created from the generic `Activity` species.
