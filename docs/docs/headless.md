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

## Before installation

Before installing COMOKIT, be sure to have on your server :

- 64 bits server
```
$ lscpu | head -n 2
Architecture:                    x86_64
CPU op-mode(s):                  32-bit, 64-bit
```
- Python 3
```
$ python3 -V
Python 3.8.2
```
- pip3
```
$ pip3 -V
pip 20.1.1 from /home/roiarthurb/.local/lib/python3.8/site-packages/pip (python 3.8)
```
- (if you don't use GAMA with JDK) JDK 8
```
$ java -version
openjdk version "1.8.0_242"
OpenJDK Runtime Environment (build 1.8.0_242-b08)
OpenJDK 64-Bit Server VM (build 25.242-b08, mixed mode)
```

### Installation

To install COMOKIT Headless on your server you can either [download a COMOKIT release](https://github.com/COMOKIT/COMOKIT-Model/releases/) and the [headless tools](https://github.com/COMOKIT/COMOKIT-HPC) or directly download the [HPC archive](https://github.com/COMOKIT/COMOKIT-HPC/releases/) (which package GAMA with an embedeed JDK, COMOKIT for Linux and the needed tools).

> If you don't use a version of GAMA provided with one of our release, be sure to use [GAMA Continuous](https://github.com/gama-platform/gama/releases/tag/continuous) and a [JAVA Developpement Kit (JDK) 8](https://en.wikipedia.org/wiki/Java_version_history#Java_SE_8)

### Setting up your server

  
To have your tooly-scripts ready to run, be sure to install all the required python's modules like so

```
$ pip3 install -r /path/to/COMOKIT-HPC/pre-processing/required.txt
```

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
