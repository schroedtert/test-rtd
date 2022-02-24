==============================================
Install JuPedSim on Windows with Visual Studio
==============================================

Visual Studio: Preparation
==========================

Before you proceed make sure your Visual Studio has some features
installed.

In our case we need ``NuGet``. So if it’s not already installed then
click

``Tools --> Get Tools and Features``

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/VSInstaller.png
   :alt: Visual studio installer

   Visual studio installer

This will start Visual Studio Installer and ask to make changes in
Visual Studio. Choose the appropriate packages and proceed.

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/installerNuGet.png
   :alt: Visual Studio NuGet

   Visual Studio NuGet

Visual Studio: Compilation
==========================

With Visual Studio open the created JPScore solution (``JPScore.sln``)
and do the following

1. ``Right click on the Solution --> Restore NuGet Packages``

   .. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/restore.png
      :alt: Restore NuGet packages

      Restore NuGet packages

   If Visual Studio offers you to restore the packages automatically, as
   shown in the following screenshot, click on ``Restore`` (and be
   patient …)

   .. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/restore_default.png
      :alt: Default restore NuGet packages

      Default restore NuGet packages

2. The project ``jpscore`` should be marked bold (important for running
   the code later on). If this is not the case, then
   ``right click on jpscore --> Set as startup Project``

   .. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/startproject.png
      :alt: Startup project

      Startup project

   After this step the project will appear bold (**jpscore**).

3. ``View --> Other Windows --> Open Package Manager Console``

   .. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/manager.png
      :alt: Package manager

      Package manager

   and type the following

   .. code:: bash

       Update-Package -reinstall -ProjectName core

   and

   .. code:: bash

       Update-Package -reinstall -ProjectName jpscore

   .. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/nuget.png
      :alt: Reinstall NuGet packages

      Reinstall NuGet packages

4. ``Build --> Build Solution``

   If this step is successful then proceed to the next step and run the
   code

5. Debug –> Start Without Debugging

   ::

      ![Run jpscore]({{ site.baseurl }}/images/vs/run.png)

   This will run jpscore in debug mode.

{% include note.html content=“this step although it runs jpscore, the
later will complain about a missing inifile” %}

6. ``Debug --> jpscore Properties --> Debugging --> Command Arguments``

   and type the full path to a demo file. For example:

   .. code:: bash

       C:\Users\here full path\demos\scenario_1_corridor\corridor_ini.xml

   .. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/cmdarg.png
      :alt: Run jpscore with demo file

      Run jpscore with demo file

Result
======

.. figure:: %7B%7B%20site.baseurl%20%7D%7D/images/vs/runjpscore.png
   :alt: Result

   Result
