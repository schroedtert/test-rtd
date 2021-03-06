---
title:  jpsreport inifile
keywords: analysis
tags: [jpsreport, file]
sidebar: jupedsim_sidebar
folder: jpsreport
summary: In the configuration file, all important information needed for the analysis are defined. For example the location of the trajectory and geometry files, the measurement methods to use, etc.
permalink: jpsreport_inifile.html
last_updated: Dec 20, 2019
---



In the configuration file, the following sections should be defined:

## Header

```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <JPSreport project="JPS-Project" version="0.8" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >
```

## Logfile
The output of the logger regarding errors, warnings and basic information is written to the console by default.
It is possible to redirect the output and write it to a file by:

```bash
./jpsreport <path_to_inifile> > log_example.txt
```

{%include note.html content="The definition of a logfile in the inifile is not supported anymore."%}

## Geometry
indicates the file name  corresponding to the trajectory files to analyze.

```xml
   <geometry file = "geo_KO_240_050_240.xml" />
```

The location can be either absolute path or relative path to the location of the inifile. A path is considered absolute if it starts with "/" (Linux system) or contains ":" (Windows system).

```xml
   <geometry file = "geo/geo_KO_240_050_240.xml" />
```

## Output
indicates the location of the output files based on the location of inifile or the absolute path.

```xml
   <output location="Output/"/>
```

A path is considered absolute if it starts with "/" (Linux system) or contains ":" (Windows system).

## Trajectories

  indicates the location and the name of the trajectory files that will be analyzed.
  The format of trajectory files should be `.txt`.

  {%include note.html content="Trajectory files in the XML format are no longer supported."%}

  The supported unit of the trajectories is `m`.
  Two other sub-options `file` and `path` can be supplied.
  If only `path` is given, then all files with the corresponding format in
  the given folder will be considered as the upcoming trajectories
  and `JPSreport` will try to load them one by one.
  If `path`is not defined, the trajectory files must be located in the same directory as the inifile.
  If both `file ` and `path` are given, then only the given trajectories
  will be considered (several `file` tags can be given at the same time).

  The location can be either absolute path or relative path to the location of the inifile.
  A path is considered absolute if it starts with "/" (Linux system) or contains ":" (Windows system).

  For example:

  ```xml
  <trajectories format="txt" unit="m">
      <file name="traj_KO_240_050_240.txt" />
      <file name="traj_KO_240_060_240.txt" />
      <path location="./" />
  </trajectories>
  ```

Do not define path information in `file` as in   

```xml
 <trajectories format="txt" unit="m">
     <file name="data/traj.txt" />
 </trajectories>
 ````  
 since this can cause issues with the output files.

## Scripts [depricated since 0.8.5]

 gives relative path based on the location of inifile or the absolute path.

  ```xml
  <scripts location="../../scripts/"/>
  ```

## Measurement area

Indicates the types and location of the measurement areas you
plan to use for analysis.
Mainly two kind of measurement areas can be defined:

- `area_B`: a 2D area and can be polygon (**the orientation of its points is clockwise**)
- `area_L`: a reference segment line defined by  two points.

`area_L` is only used in method A, while  `area_B` is used for method B, method C and method D.
Several measurement areas can be given and distinguished with different `id`. Measurement areas must be defined within one room according to the geometry file. They should not spread over several rooms or cross with walls.

The parameter `zPos` is used to indicate the position of measurement area in z axis. `zPos` is useful for geometry with several stories.

{%include note.html content="The option `length_in_movement_direction` is only used in method B and the value will be ignored in other methods. If not given in method_B, the effective distance between entrance point to the measurement area and the exit point from the measurement area will be used."%}

  ```xml
  <measurement_areas unit="m">
      <area_B id="1" type="BoundingBox" zPos="None">
          <vertex px="-2.40" py="1.00" /> <!-- Clockwise -->
          <vertex px="-2.40" py="3.00" />
          <vertex px="0" py="3.00" />
          <vertex px="0" py="1.00" />
          <length_in_movement_direction distance="2.0" />
      </area_B>
      <area_L id="2" type="Line" zPos="None">
          <start px="-2.40" py="1.00" />
          <end px="0" py="1.00" />
      </area_L>
      <area_L id="3" type="Line" zPos="None">
          <start px="-2.40" py="2.00" />
          <end px="0" py="2.00" />
      </area_L>
  </measurement_areas>
  ```
{%include note.html content="The old definition of points with the format `x=-2.40 y=1.00` is still working but deprecated. This input format will be removed in future.  "%}

## Velocity
precises the method for calculating the instantaneous velocity $$v_i(t)$$
  of pedestrian $$i$$ at time $$t$$ from trajectories:

  $$
  v_i(t) = \frac{X(t+\frac{frame\_step}{2}) - X(t-\frac{frame\_step}{2})}{frame\_step}.
  $$

```xml
  <velocity frame_step="10" set_movement_direction="None"
            ignore_backward_movement="false"/>
```

  Possible parameters are
  - `frame_step` gives the size of time interval for calculating the velocity.
    The default value is 10.
  - `set_movement_direction` indicates in which direction the velocity will be projected.
    The value of `set_movement_direction` can be:
      - `None`, which means that you don't consider the movement direction and
         calculate the velocity by the real distance. This is the default value.
      - Any real number from `0` to `360` which represents the angular information
        of the direction in the coordination system.
        Note that the axis can be represented either by `X+`, `Y+`, `X-`, `Y-` or
        by 0, 90, 180, 270.
      - `SeeTraj`. For complex trajectories with several times of direction change,
         you can indicate the detailed direction using the
         angular information in the trajectory file
         (By adding a new column in `.txt` file or adding a new variable in `.xml`
         file with the indicator `VD`).

  - `ignore_backward_movement` indicates whether you want to ignore the movement
     opposite to the direction from `set_movement_direction`.
     The default value is `false`.


## Methods

  Indicates the parameters related to each measurement method.
  Four different methods `method_A` to `method_D`are integrated in the current
  version of `JPSreport` and can be chosen for the analysis. They are used to analyze the movement of pedestrians for the steady state.
  Additionally, `Method_D` can be used for time-series analysis of individual data.


| Method | measurement area | output data |
| :---:  |     :---:        | :---:       |
| *A* | ![Method A]({{ site.baseurl }}/images/jpsreport_Method_A.png) |  $$\langle v \rangle_{\Delta t}$$ and  $$\langle J \rangle_{\Delta t}$$ |
| *B* | ![Method B]({{ site.baseurl }}/images/jpsreport_Method_B.png) | $$\langle v \rangle_i$$ and $$\langle \rho \rangle_i$$ |
| *C* | ![Method C]({{ site.baseurl }}/images/jpsreport_Method_C.png) | $$\langle v \rangle_{\Delta x}$$ and $$\langle \rho \rangle_{\Delta x}$$ |
| *D* | ![Method D]({{ site.baseurl }}/images/jpsreport_Method_D.png) | $$\langle v \rangle_v$$ and $$\langle \rho \rangle_v$$ |

  Further information relating to each method can be found
  in [Pedestrian fundamental diagrams: Comparative analysis of experiments in different geometries](http://hdl.handle.net/2128/4898).


### Method A
For definition see [Method A](jpsreport_method_A.html). Method A is used to analyze the steady state.

```xml
  <method_A enabled="true">
    <measurement_area id="2" frame_interval="100"/>
    <measurement_area id="3" frame_interval="100"/>
  </method_A>
```

Possible parameters are:
- `id` specifies the location of the reference line.
several measurement areas can be set in one inifile with different id-numbers.

- `frame_interval` specifies the size of time interval (in *frame*)
   for calculating flow rate.

- up to version 0.8.5: `plot_time_series` specifies whether output the ($$N-t$$)-Diagram.

Possible output data are:
- `/Fundamental_Diagram/FlowVelocity/`: the output files `Flow_NT_traj_` (Frame, time and cumulative pedestrians) and `FDFlowVelocity_traj_`.


### Method B
For definition see [Method B](jpsreport_method_B.html). Method B is used to analyze the steady state.

```xml
  <method_B enabled="false">
      <measurement_area id="1" />
  </method_B>
```

This method can only be used to analyze one directional (or part of one directional) pedestrian movement in corridors. The speed is defined by the length of the measurement area `length_in_movement_direction` and the time a pedestrian stays in the area.

Possible parameters are:
  - `measurement_area` given by an `id` number.
     Note that the measurement area for method_B should be
     rectangle based on the definition of the method.

Possible output data are:
  - `/Fundamental_Diagram/TinTout/`: output file `FDTinTout_traj_` with mean density and velocity of each pedestrian (PersID, $$\rho_i$$ and $$v_i$$).


### Method C
For definition see [Method C](jpsreport_method_C.html). Method C is used to analyze the steady state.

```xml
  <method_C enabled="true">
      <measurement_area id="1"/>
  </method_C>
```

Possible parameters are:

- `id` indicates the size and location of the measurement_area.
   Several measurement areas can be set in one inifile.

- up to version 0.8.5:  `plot_time_series` specifies whether output the ($$\rho-t$$) and ($$v-t$$) diagrams.


Possible output data are:
  - `/Fundamental_Diagram/Classical_Voronoi/`: output file `rho_v_Classic_traj_` with mean density and velocity of over time (frame, $$rho(t)$$, $$v(t)$$).


### Method D
For definition see [Method D](jpsreport_method_D.html). Method D is used to analyze velocity and density in the steady state as well as for time-series analysis.

```xml
 <method_D enabled="true">
   <measurement_area id="1" start_frame="None" stop_frame="None"
         local_IFD="false"/>
   <one_dimensional enabled="false"/>
   <global_IFD enabled="true"/>
   <cut_by_circle enabled="false" radius="1.0" edges="10"/>
   <profiles enabled="false" grid_size_x="0.20" grid_size_y="0.20"/>
   <use_blind_points enabled="true"/>
   <vel_calculation type="Voronoi"/>
 </method_D>
```

Possible parameters are:

- For each `measurement_area`, several id numbers can be set in one inifile.
  `start_frame` and `stop_frame` give the starting and ending frame for data analysis.
  The default values of these two parameters are `None`.
  If you plan to analysis the whole run from beginning to the end,
  set both of `start_frame` and `stop_frame` as `None`;
  If `start_frame =None` but `stop_frame` is not,
  then analysis will be performed from beginning of the trajectory to the `stop_frame`.
  If `start_frame` is not `None` but `stop_frame = None`,
  it will analyze from the `start_frame` to the end of the movement.
  `local_IFD` determines whether or not to output the data
  for individual fundamental diagram in the given measurement area,
  which is based on the Voronoi density $$\rho_i$$,  velocity $$v_i$$, position ($$x_i$$,$$y_i$$ and $$z_i$$) and Voronoi polygon
  of each pedestrian $$i$$ in a given measurement area but not mean
  value over space.
  If true, the related data will be written in the
  folder `./Output/Fundamental_Diagram/IndividualFD/`.

 - up to version 0.8.5: `plot_time_series` specifies whether output the $$\rho-t$$ and $$v-t$$-diagram.

- `one_dimensional` should be used when pedestrians move on a line
  [single-file experiment](http://www.asim.uni-wuppertal.de/datenbank/own-experiments/corridor/1d-single-file-no-2.html).

- `cut_by_circle` determines whether to cut each cell by circle or not.
         Two options `radius` of the circle and the number of `edges` have
         to be supplied for approximating the circle if `enabled` is *true*.

- up to version 0.8.5: `output_voronoi_cells` specifies whether or not to output data for visualizing
  the Voronoi diagram.
  Two options `enabled` and `plot_graphs` have to be set.
  If both of them are `true`, files including Voronoi cells,
  speed and the coordinates of pedestrian corresponding to each
  cell as well as the figures of Voronoi cells will be created in
  the folder `./Output/Fundamental_Diagram/Classical_Voronoi/VoronoiCell/`.
  If the latter is `false`, only the data will be created but the figures
  will not be plotted.
  When `enable` is `false`, nothing will be created.

- `profiles` indicates whether to calculate the profiles over time and space.
  If `enabled` is true, the resolution which is decided by the
  parameters `grid_size_x` and `grid_size_x` should be set. `start_frame` and `stop_frame` can be used to specify the time range for the analysis.
  
With this [commit](https://github.com/JuPedSim/jpscore/commit/d6ce443a4b27d0d83c05b2a77d7139c17959a224) the functionalities of Method I and J are part of Method D and can be used by configuring following parameters:

- `global_IFD` indicates a global measurement area encompassing the entire geometry for which individual data (IFD) are calculated. This parameter is set to `false`by default. `start_frame` and `stop_frame` can be used to specify the time range for the analysis.

- `use_blind_points` allows to calculate Voronoi cells in measurement areas even if less than four pedestrians are present. This is realized with the help of blind points are automatically defined outside the geometry. This parameter is set to `true`by default.

- `vel_calculation` indicates the approach that is used for the velocity calculation. By default the `Voronoi` approach is chosen but it can be changed to `Arithmetic` if needed. See [Method D](jpsreport_method_D.html) for details. 

Possible output data are:
  - `/Fundamental_Diagram/Classical_Voronoi/`: output file `rho_v_Voronoi_[velocity_calculation_type]_[filename.txt]_id_[local_measurement_area_id].dat` with mean density and velocity over time (frame, $$rho(t)$$, $$v(t)$$). 
  - `/Fundamental_Diagram/IndividualFD/`: 
    - output file `IFD_local_[filename.txt]_id_[local_measurement_area_id].dat` contains data for each pedestrian $$i$$ (in the measurement area) about individual Voronoi density $$\rho_i$$, individual velocity $$v_i$$, position ($$x_i$$,$$y_i$$ and $$z_i$$), Voronoi polygon of the pedestrian and the intersection of the Voronoi polygon with the measurement area.
    - output file `IFD_global_[filename.txt].dat` contains data for each pedestrian $$i$$ about individual Voronoi density $$\rho_i$$, individual velocity $$v_i$$, position ($$x_i$$,$$y_i$$ and $$z_i$$) and the Voronoi polygon of the pedestrian.
  - `./Output/Fundamental_Diagram/Classical_Voronoi/field/`:
    - output file `Profile_rho_Voronoi_[filename.txt]_[frame]` contains the profile data for density for one frame.
    - output file `Profile_v_[velocity_calculation_type]_[filename.txt]_[frame]` contains the profile data for velocity for one frame.
  - The output folder `./Output/Fundamental_Diagram/Classical_Voronoi/VoronoiCell/` contains the data for plotting the Voronoi cells.
  - The velocity calculation type is based on the `vel_cacluation` parameter and can be `Voronoi`or `Arithmetic`. 
