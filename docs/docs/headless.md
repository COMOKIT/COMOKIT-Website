---
layout: default
title: Headless
nav_order: 5
description: "How to use COMOKIT in headless mode on HPC."
permalink: /headless
---

# Headless
{: .no_toc }

COMOKIT has also been made to explore his model and run in headless mode on server or [HPC](https://en.wikipedia.org/wiki/High-performance_computing).
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

COMOKIT has also be developped to be runned in [headless mode](https://en.wikipedia.org/wiki/Headless_software). To do so, it's using the [GAMA Headless](https://gama-platform.github.io/wiki/Headless) feature which allows to run GAMA on a server without graphical interfaces. 

To simplify this usage, we developped some tools allowing this configuration.

## Getting started

- First, download the scripts from the [COMOKIT-HPC repository](https://github.com/COMOKIT/COMOKIT-HPC) or the direct link to clone the repository [here](https://github.com/COMOKIT/COMOKIT-HPC.git)
- decompress the downloaded archive
- open a terminal in your computer
- move inside the folder
``$ cd /path-to/COMOKIT-HPC``
- run python command to downlad the requirements
``$ pip install -r requirements.txt``

## How to use:

### Generate XML

GAMA Headless mode needs an XML configuration file in order to run GAMA. The HPC toolkit allows to generate it automatically.

- move to the folder pre-processing ``$ cd /path-to/COMOKIT-HPC/pre-processing``
- run generateMultipleXML.py with parameter to create the XML file and run GAMA. Basic usage is described bellow.

```
$ python3 generateMultipleXML.py -h
usage: generateMultipleXML.py [options] -xml <experiment name> /path/to/file.gaml /path/to/file.xml

optional arguments:
  -h, --help            show this help message and exit
  -r INT, --replication INT
                        Number of replication for each paramater space
  -s INT, --split INT   Split XML file every S replications
  -f INT, --final INT   Final step for simulations
  -o STR, --output STR  Path to folder where save output CSV
  -xml <experiment name> /path/to/file.gaml /path/to/file.xml
                        Classical xml arguments
```

**Testing Example**
```
$ python3 generateMultipleXML.py -xml "Headless" ~/COMOKIT-Model/COMOKIT/Experiments/Physical\ Interventions/Significance\ of\ Wearing\ Masks.gaml /tmp/headless/mask.xml -o ~/COMOKIT-HPC/results/ -f 2
```
**Running Example**
```
$ python3 generateMultipleXML.py -xml "Headless" ~/COMOKIT-Model/COMOKIT/Experiments/Physical\ Interventions/Significance\ of\ Wearing\ Masks.gaml /tmp/headless/mask.xml -o ~/COMOKIT-HPC/results/ -r 1000 -s 36 -f 5000
```
