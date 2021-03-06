---
title: "jpsreport: module for analysis of trajectories"
keywords: analysis
tags: [jpsreport, getting_started]
sidebar: jupedsim_sidebar
permalink: jpsreport_introduction.html
summary: This module implements different measurement methods to analyze pedestrian movement in different aspects and scales.
last_updated: Nov 09, 2021
---

[![DOI](https://zenodo.org/badge/109670242.svg)](https://zenodo.org/badge/latestdoi/109670242)

## Get started with jpsreport

`jpsreport` is a command line module to alanyse trajectories of pedestrians.
In the terminal, pass an inifile file as argument. 

The following pictures summarizes the input and output files of `jpsreport`

![Definition of input and outfile of jpsreport]({{ site.baseurl}}/images/usage_JPSreport_scaled.png)

## Preparing the input files

Three input files are required to run `jpsreport`:

- A [Configuration file](jpsreport_inifile): This inifile gives some information related to each measurement method. e. g. 
  the location of measurement areas, the chosen measurement method, etc. 
  This file should be in `.xml` format.
- A [Trajectory file](jpscore_trajectory.html): Pedestrian's 3D position information over time. 
  Only `.txt` format is supported. The file must contain the data sorted by time/frames.
- A [Geometry file](jpscore_geometry.html): Geometry for a certain trajectory data. This file should be in `.xml` format.
  

## Run jpsreport

run `jpsreport` in a terminal as follows:

```bash
./bin/jpsreport inifile.xml
```

{%include note.html content="It is possible to redirect the console output and write it to a file. See [inifile - Logfile](jpsreport_inifile#logfile)"%}

## Results

Possible output of `jpsreport` includes data for plotting fundamental diagrams, 
Voronoi diagrams and profiles of pedestrians etc. in a given geometry. 
All the output data, e.g. density and speed, 
are stored in different folders as plain text in ASCII format.


After a successful analysis additional folder named `Output` will be created in
the same directory as the used inifile. 
It contains the basic data including plain 
text and eventually figures (depending on your specifications in the inifile).


{% include links.html %}
