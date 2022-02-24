=======================
Install JuPedSim on Mac
=======================

{%include tip.html content=“to compile from the source code see the
instructions for `linux <jupedsim_install_on_linux.html>`__”%}

Homebrew installation
=====================

Homebrew users can install all packages with the following commands:

Add tap
-------

First, add jupedsim’s tap

.. code:: bash

    brew tap JuPedSim/jps

{%include note.html content=“This step is performed only once.”%}

(optional) Check dependencies
-----------------------------

First check the dependencies of the packages you want to install

.. code:: bash

    brew info <pkg>

with ``<pkg>`` is one of the available modules:

-  ``jpseditor``: geometry editor
-  ``jpscore``: simulation
-  ``jpsreport``: analysis
-  ``jpsvis``: visualisation

Install
-------

then install with

.. code:: bash

    brew install --HEAD <pkg>

(optional) Test modules
-----------------------

.. code:: bash

    brew test <pkg>

Update module
-------------

To update the installed packages use

.. code:: bash

    brew upgrade <pkg>

or reinstall it with

.. code:: bash

    brew reinstall <pkg>

{% include links.html %}
