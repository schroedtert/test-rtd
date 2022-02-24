========
Method A
========

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/jpsreport_Method_A.png
   :alt: Method A: Illustration of the measurement line.

   Method A: Illustration of the measurement line.

| A reference line is taken and studied over a fixed period of time

  .. math:: \Delta {t}

  .
| Using this method we can obtain the pedestrian flow

  .. math:: J

  \ and the velocity

  .. math:: v_i

  of each pedestrian passing the reference line directly. Thus, the flow
  over time

  .. math:: \langle J \rangle_{\Delta t}

  and the time mean velocity

  .. math:: \langle v \rangle_{\Delta t}

  can be calculated as

.. math:: \langle J \rangle_{\Delta t}=\frac{N^{\Delta t}}{t_N^{\Delta t} - t_1^{\Delta t}}\qquad \text{and} \qquad \langle v \rangle_{\Delta t}=\frac{1}{N^{\Delta t}}\sum_{i=1}^{N^{\Delta t}} v_i(t),

where

.. math:: N^{\Delta t}

\ is the number of persons passing the reference line during the time
interval

.. math:: \Delta {t}

.

.. math:: t_N^{\Delta {t}}

\ and

.. math:: t_1^{\Delta {t}}

are the times when the first and last pedestrians pass the location in

.. math:: \Delta {t}

.

{%include note.html content=“Note: this time period can be different
from

.. math:: \Delta {t}

.”%}

The time mean velocity

.. math:: \langle v \rangle_{\Delta t}

\ is defined as the mean value of the instantaneous velocities

.. math:: N^{\Delta t}

pedestrians.

.. math:: v_i(t)

\ is calculated by use of the displacement of pedestrian

.. math:: i

in a small time interval

.. math:: \Delta t^\prime

around

.. math:: t

:

.. math:: v_i(t)=\frac{\vec{x_i}(t+\Delta t^\prime/2)-\vec{x_i}(t-\Delta t^\prime/2))}{\Delta t^\prime}.
