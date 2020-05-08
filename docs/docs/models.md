---
layout: default
title: Models used in COMOKIT
nav_order: 4
permalink: /modelsUsed
---

# Models used in COMOKIT
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## The Agent-Based Model 

Here's an early draft of the UML graph of our model

![UML](assets/images/general-uml.png)

## The epidemiological model

In our model, our _People_ agent follow a slightly modified [SEIR model](https://en.wikipedia.org/wiki/Compartmental_models_in_epidemiology#The_SEIR_model).

![SEIR](assets/images/Epidemic-model-agent.png)

Incubation, serial and infectious periods follow various distributions.
![SEIR](assets/images/IncubationPeriod.png)
![SEIR](assets/images/Serial-Infectious-Distribution.png)