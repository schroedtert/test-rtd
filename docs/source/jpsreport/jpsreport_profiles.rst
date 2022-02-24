================
Density profiles
================

{%include note.html content=“this tutorial needs links to data”%}

Here is an example extracted from a T-Junction experiment:

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/Figue4-4-3.png
   :alt: T-junction

   T-junction

Run jpsreport
=============

| In order to calculate the profiles it is mandatory to use `method
  D <jpsreport_method_D.html>`__ or `method
  I <jpsreport_method_I.html>`__.
| M oreover, Set the parameter ``enabled`` of profiles to ``true``.
| Set the resolution of the profile by initializing the two parameters
  ``grid_size_x``\ and ``grid_size_y``, e.g.:

.. code:: xml

    <method_D enabled="true"> 
      <profiles enabled="true" grid_size_x="0.20" grid_size_y="0.20"/> 
    </method_D> 

(optional) Steady state
=======================

Determine the steady state of the experiment in the whole measurement
region. In the folder script there is a script to fulfill this task
semi-manually.

Produce the profiles
====================

Run the python script ``_Plot_profiles.py``, which is in the scripts
folder in ``jpsreport``.
