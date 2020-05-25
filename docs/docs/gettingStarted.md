---
layout: default
title: Getting Started
nav_order: 2
permalink: /gettingStarted
---

# Getting Started
{: .no_toc }


How to run COMOKIT locally
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Download the latest COMOKIT Release

The base model represents the diffusion and transmission of COVID-19 at the scale of a commune (approx. 10.000 people in Vietnam) using an agent-based approach: each inhabitant is represented individually with his/her specific characteristics (age, sex, household), clinical state (susceptible, exposed, infected with or w/o symptoms, recovered or dead) and daily activities based on a generated agenda, which can be controlled and limited by an Authority agent whose role is to choose and apply a public health policy consisting of mitigation measures and interventions. Each set of parameters (incl. the policies applied) represents a scenario, which can be explored by running several simulations (to account for the stochasticity of each run) and compared against other scenarios in more elaborate experiments. COMOKIT makes it therefore very easy to assess, measure and compare the impacts of interventions on the spread of the virus. The data required to instantiate this base model on a specific case study is voluntarily limited; in most cases, only a file containing the built environment may be enough to build a simple model. More realistic scenarios will of course require more detailed datasets.

## Install it yourself

If you want to install and run the model yourself on your computer you should 

- First, download and extract the [GAMA Continuous Build version](https://github.com/gama-platform/gama/releases/tag/continuous) (if you don't know which version to take, choose the one with JDK). If you need more information about how to install GAMA, check the [installation page](https://gama-platform.github.io/wiki/Installation)
- Second download the model [on GitHub](https://github.com/COMOKIT/CoVid19) (click [here](https://github.com/COMOKIT/CoVid19/archive/master.zip) to download it automatically)
- Extract that ZIP file somewhere on your computer and [import it on GAMA](https://gama-platform.github.io/wiki/ImportingModels) as a GAMA project.
<img src='https://gama-platform.github.io/resources/images/workspaceProjectsAndModels/import_menu_file_import.png' alt='Import a Gama project' width='600'/>
<br>
<img src='https://gama-platform.github.io/resources/images/workspaceProjectsAndModels/import_dialog_import_projects.png' alt='Import a Gama project from a folder' width='600'/>

## How to run

- select an experiment to run. Bellow we selected the *Realistic Lockdown Durations.gaml* experiment.

<p align="center">
  <img  src="assets/images/Gama-launching-experiment.png?raw=true">
</p>
