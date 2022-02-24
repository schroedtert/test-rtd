========
Method B
========

The spatial mean velocity and density are calculated by taking a segment

.. math:: \Delta x

\ in a corridor as the measurement area.

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/jpsreport_Method_B.png
   :alt: Method B: Illustration of the measurement interval.

   Method B: Illustration of the measurement interval.

The velocity

.. math:: \langle v \rangle_i

\ of each person is defined as the length

.. math:: \Delta x

of the measurement area divided by the time he or she needs to cross the
area:

.. math:: \langle v \rangle_i=\frac{\Delta x}{t_\text{out}-t_\text{in}},

where

.. math:: t_\text{in}

\ and

.. math:: t_\text{out}

are the times a person enters and exits the measurement area,
respectively.

The density

.. math:: \rho_i

\ for each person

.. math:: i

is calculated as:

.. math:: \langle \rho \rangle_i=\frac{1}{t_\text{out}-t_\text{in}}\cdot\int_{t_\text{in}}^{t_\text{out}} \frac{N^\prime(t)}{b_\text{cor}\cdot\Delta x}dt,

where

.. math:: b_\text{cor}

\ is the width of the measurement area while

.. math:: N^\prime(t)

is the number of person in this area at a time

.. math:: t

.
