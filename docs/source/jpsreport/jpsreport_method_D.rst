========
Method D
========

At any time the positions of the pedestrians can be represented as a set
of points, from which the Voronoi diagram can be generated.

The Voronoi cell area,

.. math:: A_i

, for each person

.. math:: i

can be obtained.

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/jpsreport_Method_D.png
   :alt: Method D: Illustration of the Voronoi diagrams

   Method D: Illustration of the Voronoi diagrams

Then, the density and velocity distribution of the space

.. math:: \rho_{xy} 

\ and

.. math:: v_{xy}

can be defined as

.. math:: \rho_{xy} = 1/A_i \quad \text{and} \quad v_{xy}={v_i(t)}\qquad \mbox{if} (x,y) \in A_i,

where

.. math:: v_i(t)

\ is the instantaneous velocity of each person.

The **Voronoi density** for the measurement area is defined as:

.. math:: \langle \rho \rangle_v=\frac{\iint{\rho_{xy}dxdy}}{b_\text{cor}\cdot\Delta x}.

For a given trajectory

.. math:: \vec{x_i}(t)

, the velocity

.. math:: v_i(t)

is calculated by use of the displacement of pedestrian

.. math:: i

in a small time interval

.. math:: \Delta t^\prime

around

.. math:: t

:

.. math:: v_i(t)=\frac{\vec{x_i}(t+\Delta t^\prime/2)-\vec{x_i}(t-\Delta t^\prime/2))}{\Delta t^\prime}.

For calculating the mean velocity in the measurement area two approaches
can be applied.

1. The **Voronoi velocity** is defined as:

.. math:: \langle v \rangle_v=\frac{\iint{v_{xy}dxdy}}{b_\text{cor}\cdot\Delta x}.

2. The **Arithmetic velocity** is the average of the instantaneous
   velocities

   .. math:: v_i(t)

   \ for all pedestrians

   .. math:: N

   who have an intersection with the measurement area at the time

   .. math:: t

   :

.. math:: \langle v \rangle_{\Delta x}=\frac{1}{N_{(x,y) \in A_i}}\sum_{i=1}^{N_{(x,y) \in A_i}}{v_i(t)}.
