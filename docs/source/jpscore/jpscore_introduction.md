---
title: "Getting started with jupedsim"
keywords: simulation
tags: [jpscore, getting_started]
sidebar: jupedsim_sidebar
permalink: jpscore_introduction.html
summary: jpscore is the simulation module of JuPedSim. It's a command-line tool to simulate the evacuation of pedestrians in continuous space.
last_updated: Nov 09, 2021
toc: false
---

[![DOI](https://zenodo.org/badge/36440436.svg)](https://zenodo.org/badge/latestdoi/36440436)

`jpscore` implements models on the operational as well as on the tactical level of pedestrian dynamics.

## Demo files

In the directory `demos` there are some examples to start with:


```bash
├── demos
│   ├── scenario_1_corridor
│   │   ├── corridor_geo.xml
│   │   ├── corridor_ini.xml
│   ├── scenario_2_bottleneck
│   │   ├── bottleneck_geo.xml
│   │   └── bottleneck_ini.xml
│   ├── scenario_3_corner
│   │   ├── corner_geo.xml
│   │   ├── corner_ini.xml
│   │   └── corner_routing.xml
│   ├── scenario_4_stairs
│   │   ├── stairs_geo.xml
│   │   ├── stairs_ini.xml
│   │   └── stairs_routing.xml
    │   ├── scenario_7_floorfield
│   │   ├── Kobes_geo.xml
│   │   ├── ffRouter_ini.xml
|
|
|.....
│

```

Taking the 7th demo as input, we run a simulation as follows:

```bash
 ./bin/jpscore  demos/corner_ini.xml
```

Information on processing steps, warnings and errors of jpscore are written to the console. This output can be redirected to a file by:

```bash
 ./bin/jpscore  demos/corner_ini.xml > log_example.txt
```

This program call produces a trajectory file in the folder `results` in the same directory. This can be visualized with `jpsvis`

```bash
 jpsvis demos/scenario_7_floorfield/results/Kobes_traj.xml
```


![Simulation using demo 7 of `jpscore` ]({{ site.baseurl  }}/images/kobe.gif)


{% include links.html %}
