---
layout: default
title: Home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# COMOKIT

IRD, the developers of GAMA and their partners in Vietnam are supporting Vietnamese authorities in their fight against the COVID-19 pandemic by developping a complete modeling platform named COMOKIT, which aims at assessing and comparing mitigation policies and interventions against the spread of the virus.

# Introduction

> Is the containment of a neighborhood more effective than that of an entire village/town? Does school closure reduce the transmission peaks ? What is the most effective strategy to adopt when resources are limited (e.g. enforcement of the rules, capacity of hospitals) ? When to start a containment policy and how long should it last to be effective ?

These are some of the questions adressed by this generic integrated model, which combines a sub-model of the individual clinical dynamics and epidemiological status of agents, a sub-model of agent-to-agent direct transmission of the infection, a sub-model of environmental transmission through the built environment, a sub-model of policy design and implementation, and an agenda-based model of people activities at a one-hour time step.

# The team working on this project

The Institut de recherche pour le développement (IRD) in Vietnam has set up a multidisciplinary team of researchers from its research units UMMISCO (Alexis Drogoul, Benoit Gaudou, Arthur Brugière, Kevin Chapuis), MIVEGEC (Marc Choisy) and DIADE (Pierre Larmande), assisted by colleagues from Thuyloi University (Nguyen Ngoc Doanh), Can Tho University (Huỳnh Quang Nghi), INRAE (Patrick Taillandier) and SPH-HKU (Damien Philippon), to design realistic spatial computer models, in GAMA, from the data provided by the government (census, epidemiological data) or obtained from private actors (Facebook data, mobile telephone data) in order to inform as quickly as possible the public health decisions taken by the Vietnamese authorities, in particular those linked to the impact of containment strategies when cases are detected.

# Base model

The base model represents the diffusion and transmission of COVID-19 at the scale of a commune (approx. 10.000 people in Vietnam) using an agent-based approach: each inhabitant is represented individually with his/her specific characteristics (age, sex, household), clinical state (susceptible, exposed, infected with or w/o symptoms, recovered or dead) and daily activities based on a generated agenda, which can be controlled and limited by an Authority agent whose role is to choose and apply a public health policy consisting of mitigation measures and interventions. Each set of parameters (incl. the policies applied) represents a scenario, which can be explored by running several simulations (to account for the stochasticity of each run) and compared against other scenarios in more elaborate experiments. COMOKIT makes it therefore very easy to assess, measure and compare the impacts of interventions on the spread of the virus. The data required to instantiate this base model on a specific case study is voluntarily limited; in most cases, only a file containing the built environment may be enough to build a simple model. More realistic scenarios will of course require more detailed datasets.