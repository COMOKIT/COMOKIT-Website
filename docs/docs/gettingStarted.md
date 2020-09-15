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

## Install COMOKIT

You can install and run COMOKIT by two ways: 
- you can download and run the _All-In-One_ archive, 
- you can manually install GAMA (1.8.1 or above) and import COMOKIT inside. 

> We do recommend you to pick the first option (especially if you are a beginner).

## Bundled install (easy)

- First you should [download the All-In-One](https://github.com/COMOKIT/COMOKIT-Model/releases/latest) archive for your system (Windows, MacOS or Linux).
- Unzip it on your computer (the place is not important).
- Open the extracted folder.
- Start the GAMA Application.

Here you are, you have an instance of COMOKIT running on your computer.

![Empty GAMA - COMOKIT](assets/images/GAMAxCOMOKIT-raw.png)

### Manual install (harder)

If you want to install and run the model yourself on your computer you should: 

- First, download and extract the [GAMA 1.8.1 version](https://github.com/gama-platform/gama/releases/tag/1.8.1) or [above](https://github.com/gama-platform/gama/releases) (if you do not know which version to take, choose the one with JDK). If you need more information about how to install GAMA, check the [installation page](https://gama-platform.github.io/wiki/Installation)
- Second, download the model [on GitHub](https://github.com/COMOKIT/COMOKIT-Model) (click [here](https://github.com/COMOKIT/COMOKIT-Model/archive/master.zip) to download it automatically)
- Extract that ZIP file somewhere on your computer and [import it on GAMA](https://gama-platform.github.io/wiki/ImportingModels) as a GAMA project (see pictures below).

![Import a Gama project](https://gama-platform.github.io/resources/images/workspaceProjectsAndModels/import_menu_file_import.png)

![Import a Gama project from a folder](https://gama-platform.github.io/resources/images/workspaceProjectsAndModels/import_dialog_import_projects.png)

## How to run

- Launch your installed GAMA application
- Select an experiment to run. Bellow we selected the *COMOKIT/Experiments/Lockdown/Realistic Lockdown Durations.gaml* experiment.

![Realistic Lockdown Durations.gaml](assets/images/Gama-launching-experiment.png?raw=true)

- Click on the *Early containment* green button to run this experiment.
- Select which city to run the experiment on.

![Pick dataset](assets/images/Gama-launching-experiment-validation.png?raw=true)

- GAMA will take a few seconds (depending on your computer power) to create the various simulations and displays. You should finally observe the following picture and the simulations run automatically.

![Pick dataset](assets/images/Gama-COMOKIT-lockdown-experiment-launched.png?raw=true)
