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

You can install and run COMOKIT by two way : you can download and run the _All-In-One_ archive, or manually install GAMA and import COMOKIT inside. 

> We do recommend you to pick the first option (especially if you're a beginner).

## Bundled install (easy)

<details>
	<summary style="display: list-item">View contents</summary>

- First you should [download the All-In-One](https://github.com/COMOKIT/COMOKIT-Model/releases/tag/v1.0) archive for your system (Windows, MacOS or Linux).
- Unzip it on your computer (the place isn't important, but do know where).
- Open the extracted folder.
- Start the GAMA Application.

Here you are, you have an instance of COMOKIT running on your computer.

</details>

### Manual install (harder)

<details>
	<summary style="display: list-item">View contents</summary>

If you want to install and run the model yourself on your computer you should 

- First, download and extract the [GAMA Continuous Build version](https://github.com/gama-platform/gama/releases/tag/continuous) (if you don't know which version to take, choose the one with JDK). If you need more information about how to install GAMA, check the [installation page](https://gama-platform.github.io/wiki/Installation)
- Second download the model [on GitHub](https://github.com/COMOKIT/COMOKIT-Model) (click [here](https://github.com/COMOKIT/COMOKIT-Model/archive/master.zip) to download it automatically)
- Extract that ZIP file somewhere on your computer and [import it on GAMA](https://gama-platform.github.io/wiki/ImportingModels) as a GAMA project.

![Import a Gama project](https://gama-platform.github.io/resources/images/workspaceProjectsAndModels/import_menu_file_import.png)

![Import a Gama project from a folder](https://gama-platform.github.io/resources/images/workspaceProjectsAndModels/import_dialog_import_projects.png)

</details>

## How to run

- Launch your installed GAMA application
- Select an experiment to run. Bellow we selected the *COMOKIT/Experiments/Lockdown/Realistic Lockdown Durations.gaml* experiment.

![Realistic Lockdown Durations.gaml](https://github.com/COMOKIT/COMOKIT-Website/blob/master/docs/assets/images/Gama-launching-experiment.png?raw=true)

- Click on the *Early containment* green button to run this experiment.
- Select which city to run the experiment on.

![Pick dataset](assets/images/Gama-launching-experiment-validation.png?raw=true)
