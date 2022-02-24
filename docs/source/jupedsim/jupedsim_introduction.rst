========
JuPedSim
========

This software is platform independent, released under the LGPL license
and is written in C++ and Python.

Goal
====

The primary goal of ``JuPedSim`` is to provide students and researchers
with a framework to investigate pedestrian dynamics and focus on
research, i.e. development and validation of new models or model
features, analysis of experiments and proper visualization of results.

``JuPedSim`` is currently focusing on evacuation, but is easily
extendable to cover other areas e.g. passengers exchange, commuter
traffic in railway stations etc.

Organization of the code
========================

``JuPedSim`` consists of four loosly coupled modules, that can be used
independently. These are:

1. ``jpscore``: the core module computing the trajectories.
2. ``jpsreport``: a tool for analyzing the trajectories and validating
   the model.
3. ``jpsvis``: a tool for visualizing the input (geometry) and output
   (trajectories) data.
4. ``jpseditor``: a tool for creating and editing geometry files with
   dxf import/export capabilities.

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/structure.png
   :alt: Structure of JuPedSim: interacting modules

   Structure of JuPedSim: interacting modules

Showcase and tutorials
======================

To highlight some features of ``JuPedSim`` we have uploaded some videos
and tutorials on our `YouTube
channel <https://www.youtube.com/channel/UCKS8w8CUClHEeN4K1SUSMBA>`__.

{% include links.html %}
