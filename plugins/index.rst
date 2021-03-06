.. _plugins:

Navigation Plugins
##################

There are a number of plugin interfaces for users to create their own custom applications or algorithms with.
Namely, the costmap layer, planner, controller, behavior tree, and recovery plugins.
A list of all known plugins are listed here below for ROS 2 Navigation.
If you know of a plugin, or you have created a new plugin, please consider submitting a pull request with that information.

This file can be found and editted under ``sphinx_docs/plugins/index.rst``.
For tutorials on creating your own plugins, please see :ref:`writing_new_costmap2d_plugin`, :ref:`writing_new_nbt_plugin`, :ref:`writing_new_nav2controller_plugin`, :ref:`writing_new_nav2planner_plugin`, or :ref:`writing_new_recovery_plugin`.

Costmap Layers
==============

+--------------------------------+------------------------+----------------------------------+
|            Plugin Name         |         Creator        |       Description                |
+================================+========================+==================================+
| `Voxel Layer`_                 | Eitan Marder-Eppstein  | Maintains persistant             |
|                                |                        | 3D voxel layer using depth and   |
|                                |                        | laser sensor readings and        |
|                                |                        | raycasting to clear free space   |
+--------------------------------+------------------------+----------------------------------+
| `Range Layer`_                 | David Lu               | Uses a probabalistic model to    |
|                                |                        | put data from sensors that       |
|                                |                        | publish range msgs on the costmap|
+--------------------------------+------------------------+----------------------------------+
| `Static Layer`_                | Eitan Marder-Eppstein  | Gets static ``map`` and loads    |
|                                |                        | occupancy information into       |
|                                |                        | costmap                          |
+--------------------------------+------------------------+----------------------------------+
| `Inflation Layer`_             | Eitan Marder-Eppstein  | Inflates lethal obstacles in     |
|                                |                        | costmap with exponential decay   |
+--------------------------------+------------------------+----------------------------------+
|  `Obstacle Layer`_             | Eitan Marder-Eppstein  | Maintains persistent 2D costmap  |
|                                |                        | from 2D laser scans with         |
|                                |                        | raycasting to clear free space   |
+--------------------------------+------------------------+----------------------------------+
| `Spatio-Temporal Voxel Layer`_ |  Steve Macenski        | Maintains temporal 3D sparse     |
|                                |                        | volumetric voxel grid with decay |
|                                |                        | through sensor models            |
+--------------------------------+------------------------+----------------------------------+
| `Non-Persistent Voxel Layer`_  |  Steve Macenski        | Maintains 3D occupancy grid      |
|                                |                        | consisting only of the most      |
|                                |                        | sets of measurements             |
+--------------------------------+------------------------+----------------------------------+

.. _Voxel Layer: https://github.com/ros-planning/navigation2/tree/main/nav2_costmap_2d/plugins/voxel_layer.cpp
.. _Static Layer: https://github.com/ros-planning/navigation2/tree/main/nav2_costmap_2d/plugins/static_layer.cpp
.. _Range Layer: https://github.com/ros-planning/navigation2/tree/main/nav2_costmap_2d/plugins/range_sensor_layer.cpp
.. _Inflation Layer: https://github.com/ros-planning/navigation2/tree/main/nav2_costmap_2d/plugins/inflation_layer.cpp
.. _Obstacle Layer: https://github.com/ros-planning/navigation2/tree/main/nav2_costmap_2d/plugins/obstacle_layer.cpp
.. _Spatio-Temporal Voxel Layer: https://github.com/SteveMacenski/spatio_temporal_voxel_layer/
.. _Non-Persistent Voxel Layer: https://github.com/SteveMacenski/nonpersistent_voxel_layer

Costmap Filters
===============

+--------------------+--------------------+-----------------------------------+
|    Plugin Name     |      Creator       |       Description                 |
+====================+====================+===================================+
| `Keepout Filter`_  | Alexey Merzlyakov  | Maintains keep-out/safety zones   |
|                    |                    | and preferred lanes for moving    |
+--------------------+--------------------+-----------------------------------+

.. _Keepout Filter: https://github.com/ros-planning/navigation2/tree/main/nav2_costmap_2d/plugins/costmap_filters/keepout_filter.cpp

Controllers
===========

+--------------------------+--------------------+----------------------------------+-----------------------+
|      Plugin Name         |       Creator      |       Description                | Drivetrain support    |
+==========================+====================+==================================+=======================+
|  `DWB Controller`_       | David Lu!!         | A highly configurable  DWA       | Differential,         |
|                          |                    | implementation with plugin       | Omnidirectional,      |
|                          |                    | interfaces                       | Legged                |
+--------------------------+--------------------+----------------------------------+-----------------------+
|  `TEB Controller`_       | Christoph Rösmann  | A MPC-like controller suitable   | **Ackermann**, Legged,|
|                          |                    | for ackermann, differential, and | Omnidirectional,      |
|                          |                    | holonomic robots.                | Legged,               |
+--------------------------+--------------------+----------------------------------+-----------------------+

.. _DWB Controller: https://github.com/ros-planning/navigation2/tree/main/nav2_dwb_controller
.. _TEB Controller: https://github.com/rst-tu-dortmund/teb_local_planner

Planners
========

+-------------------+---------------------------------------+------------------------------+---------------------+
| Plugin Name       |         Creator                       |       Description            | Drivetrain support  |
+===================+=======================================+==============================+=====================+
|  `NavFn Planner`_ | Eitan Marder-Eppstein & Kurt Konolige | A navigation function        | Differential,       |
|                   |                                       | using A* or Dijkstras        | Omnidirectional,    |
|                   |                                       | expansion, assumes 2D        | Legged              |
|                   |                                       | holonomic particle           |                     |
+-------------------+---------------------------------------+------------------------------+---------------------+
|  `SmacPlanner`_   | Steve Macenski                        | A SE2 Hybrid-A*              | **Ackermann**,      |
|                   |                                       | implementation using either  | Differential,       |
|                   |                                       | Dubin or Reeds-shepp motion  | Omnidirectional,    |
|                   |                                       | models with smoother and     | Legged              |
|                   |                                       | multi-resolution query.      |                     |
|                   |                                       | Cars, car-like, and          |                     |
|                   |                                       | ackermann vehicles.          |                     |
+-------------------+---------------------------------------+------------------------------+---------------------+
|  `SmacPlanner2D`_ | Steve Macenski                        | A 2D A* implementation       | Differential,       |
|                   |                                       | Using either 4 or 8          | Omnidirectional,    |
|                   |                                       | connected neighborhoods      | Legged              |
|                   |                                       | with smoother and            |                     |
|                   |                                       | multi-resolution query       |                     |
+-------------------+---------------------------------------+------------------------------+---------------------+

.. _NavFn Planner: https://github.com/ros-planning/navigation2/tree/main/nav2_navfn_planner
.. _SmacPlanner: https://github.com/ros-planning/navigation2/tree/main/nav2_smac_planner
.. _SmacPlanner2D: https://github.com/ros-planning/navigation2/tree/main/nav2_smac_planner

Recoveries
==========

+----------------------+------------------------+----------------------------------+
|  Plugin Name         |         Creator        |       Description                |
+======================+========================+==================================+
|  `Clear Costmap`_    | Eitan Marder-Eppstein  | A service to clear the given     |
|                      |                        | costmap in case of incorrect     |
|                      |                        | perception or robot is stuck     |
+----------------------+------------------------+----------------------------------+
|  `Spin`_             | Steve Macenski         | Rotate recovery of configurable  |
|                      |                        | angles to clear out free space   |
|                      |                        | and nudge robot out of potential |
|                      |                        | local failures                   |
+----------------------+------------------------+----------------------------------+
|    `Back Up`_        | Brian Wilcox           | Back up recovery of configurable |
|                      |                        | distance to back out of a        |
|                      |                        | situation where the robot is     |
|                      |                        | stuck                            |
+----------------------+------------------------+----------------------------------+
|             `Wait`_  | Steve Macenski         | Wait recovery with configurable  |
|                      |                        | time to wait in case of time     |
|                      |                        | based obstacle like human traffic|
|                      |                        | or getting more sensor data      |
+----------------------+------------------------+----------------------------------+

.. _Back Up: https://github.com/ros-planning/navigation2/tree/main/nav2_recoveries/plugins
.. _Spin: https://github.com/ros-planning/navigation2/tree/main/nav2_recoveries/plugins
.. _Wait: https://github.com/ros-planning/navigation2/tree/main/nav2_recoveries/plugins
.. _Clear Costmap: https://github.com/ros-planning/navigation2/blob/main/nav2_costmap_2d/src/clear_costmap_service.cpp

Waypoint Task Executors
=======================

+---------------------------------+------------------------+----------------------------------+
|        Plugin Name              |         Creator        |       Description                |
+=================================+========================+==================================+
| `WaitAtWaypoint`_               | Fetullah Atas          | A plugin to execute a wait       |
|                                 |                        | behavior  on                     |
|                                 |                        | waypoint arrivals.               |
|                                 |                        |                                  |
+---------------------------------+------------------------+----------------------------------+
| `PhotoAtWaypoint`_              | Fetullah Atas          | A plugin to take and save photos |
|                                 |                        | to specified directory on        |
|                                 |                        | waypoint arrivals.               |
|                                 |                        |                                  |
+---------------------------------+------------------------+----------------------------------+
| `InputAtWaypoint`_              | Steve Macenski         | A plugin to wait for user input  |
|                                 |                        | before moving onto the next      |
|                                 |                        | waypoint.                        |
+---------------------------------+------------------------+----------------------------------+

.. _WaitAtWaypoint: https://github.com/ros-planning/navigation2/tree/main/nav2_waypoint_follower/plugins/wait_at_waypoint.cpp
.. _PhotoAtWaypoint: https://github.com/ros-planning/navigation2/tree/main/nav2_waypoint_follower/plugins/photo_at_waypoint.cpp
.. _InputAtWaypoint: https://github.com/ros-planning/navigation2/tree/main/nav2_waypoint_follower/plugins/input_at_waypoint.cpp

Goal Checkers
=============

+---------------------------------+------------------------+----------------------------------+
|     Plugin Name                 |         Creator        |       Description                |
+=================================+========================+==================================+
| `SimpleGoalChecker`_            | David Lu!!             | A plugin check whether robot     |
|                                 |                        | is within translational distance |
|                                 |                        | and rotational distance of goal. |
|                                 |                        |                                  |
+---------------------------------+------------------------+----------------------------------+
| `StoppedGoalChecker`_           | David Lu!!             | A plugin check whether robot     |
|                                 |                        | is within translational distance |
|                                 |                        | , rotational distance of goal,   |
|                                 |                        | and velocity threshold.          |
+---------------------------------+------------------------+----------------------------------+

.. _SimpleGoalChecker: https://github.com/ros-planning/navigation2/blob/main/nav2_controller/plugins/simple_goal_checker.cpp
.. _StoppedGoalChecker: https://github.com/ros-planning/navigation2/blob/main/nav2_controller/plugins/stopped_goal_checker.cpp

Progress Checkers
=================

+---------------------------------+------------------------+----------------------------------+
|         Plugin Name             |         Creator        |       Description                |
+=================================+========================+==================================+
| `SimpleProgressChecker`_        | David Lu!!             | A plugin to check whether the    |
|                                 |                        | robot was able to move a minimum |
|                                 |                        | distance in a given time to      |
|                                 |                        | make progress towards a goal     |
+---------------------------------+------------------------+----------------------------------+

.. _SimpleProgressChecker: https://github.com/ros-planning/navigation2/blob/main/nav2_controller/plugins/simple_progress_checker.cpp


Behavior Tree Nodes
===================

+--------------------------------------------+---------------------+----------------------------------+
| Action Plugin Name                         |   Creator           |       Description                |
+============================================+=====================+==================================+
| `Back Up Action`_                          | Michael Jeronimo    | Calls backup recovery action     |
+--------------------------------------------+---------------------+----------------------------------+
| `Clear Costmap Service`_                   | Carl Delsey         | Calls clear costmap service      |
+--------------------------------------------+---------------------+----------------------------------+
| `Compute Path to Pose Action`_             | Michael Jeronimo    | Calls Nav2 planner server        |
+--------------------------------------------+---------------------+----------------------------------+
| `Follow Path Action`_                      | Michael Jeronimo    | Calls Nav2 controller server     |
+--------------------------------------------+---------------------+----------------------------------+
| `Navigate to Pose Action`_                 | Michael Jeronimo    | BT Node for other                |
|                                            |                     | BehaviorTree.CPP BTs to call     |
|                                            |                     | Navigation2 as a subtree action  |
+--------------------------------------------+---------------------+----------------------------------+
| `Reinitalize Global Localization Service`_ | Carl Delsey         | Reinitialize AMCL to a new pose  |
+--------------------------------------------+---------------------+----------------------------------+
| `Spin Action`_                             | Carl Delsey         | Calls spin recovery action       |
+--------------------------------------------+---------------------+----------------------------------+
| `Wait Action`_                             | Steve Macenski      | Calls wait recovery action       |
+--------------------------------------------+---------------------+----------------------------------+
| `Truncate Path`_                           | Francisco Martín    | Modifies a path making it shorter|
+--------------------------------------------+---------------------+----------------------------------+

.. _Back Up Action: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/back_up_action.cpp
.. _Clear Costmap Service: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/clear_costmap_service.cpp
.. _Compute Path to Pose Action: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/compute_path_to_pose_action.cpp
.. _Follow Path Action: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/follow_path_action.cpp
.. _Navigate to Pose Action: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/navigate_to_pose_action.cpp
.. _Reinitalize Global Localization Service: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/reinitialize_global_localization_service.cpp
.. _Spin Action: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/spin_action.cpp
.. _Wait Action: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/wait_action.cpp
.. _Truncate Path: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/action/truncate_path_action.cpp


+------------------------------------+--------------------+------------------------+
| Condition Plugin Name              |         Creator    |       Description      |
+====================================+====================+========================+
| `Goal Reached Condition`_          | Carl Delsey        | Checks if goal is      |
|                                    |                    | reached within tol.    |
+------------------------------------+--------------------+------------------------+
| `Goal Updated Condition`_          |Aitor Miguel Blanco | Checks if goal is      |
|                                    |                    | preempted.             |
+------------------------------------+--------------------+------------------------+
| `Initial Pose received Condition`_ | Carl Delsey        | Checks if initial pose |
|                                    |                    | has been set           |
+------------------------------------+--------------------+------------------------+
| `Is Stuck Condition`_              |  Michael Jeronimo  | Checks if robot is     |
|                                    |                    | making progress or     |
|                                    |                    | stuck                  |
+------------------------------------+--------------------+------------------------+
| `Transform Available Condition`_   |  Steve Macenski    | Checks if a TF         |
|                                    |                    | transformation is      |
|                                    |                    | available. When        |
|                                    |                    | succeeds returns       |
|                                    |                    | success for subsequent |
|                                    |                    | calls.                 |
+------------------------------------+--------------------+------------------------+
| `Distance Traveled Condition`_     |  Sarthak Mittal    | Checks is robot has    |
|                                    |                    | traveled a given       |
|                                    |                    | distance.              |
+------------------------------------+--------------------+------------------------+
| `Time Expired Condition`_          |  Sarthak Mittal    | Checks if a given      |
|                                    |                    | time period has        |
|                                    |                    | passed.                |
+------------------------------------+--------------------+------------------------+
| `Is Battery Low Condition`_        |  Sarthak Mittal    | Checks if battery      |
|                                    |                    | percentage is below    |
|                                    |                    | a specified value.     |
+------------------------------------+--------------------+------------------------+

.. _Goal Reached Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/goal_reached_condition.cpp
.. _Goal Updated Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/goal_updated_condition.cpp
.. _Initial Pose received Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/initial_pose_received_condition.cpp
.. _Is Stuck Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/is_stuck_condition.cpp
.. _Transform Available Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/transform_available_condition.cpp
.. _Distance Traveled Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/distance_traveled_condition.cpp
.. _Time Expired Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/time_expired_condition.cpp
.. _Is Battery Low Condition: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/condition/is_battery_low_condition.cpp

+--------------------------+-------------------+----------------------------------+
| Decorator Plugin Name    |    Creator        |       Description                |
+==========================+===================+==================================+
| `Rate Controller`_       | Michael Jeronimo  | Throttles child node to a given  |
|                          |                   | rate                             |
+--------------------------+-------------------+----------------------------------+
| `Distance Controller`_   | Sarthak Mittal    | Ticks child node based on the    |
|                          |                   | distance traveled by the robot   |
+--------------------------+-------------------+----------------------------------+
| `Speed Controller`_      | Sarthak Mittal    | Throttles child node to a rate   |
|                          |                   | based on current robot speed.    |
+--------------------------+-------------------+----------------------------------+
| `Goal Updater`_          | Francisco Martín  | Updates the goal received via    |
|                          |                   | topic subscription.              |
+--------------------------+-------------------+----------------------------------+

.. _Rate Controller: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/decorator/rate_controller.cpp
.. _Distance Controller: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/decorator/distance_controller.cpp
.. _Speed Controller: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/decorator/speed_controller.cpp
.. _Goal Updater: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/decorator/goal_updater_node.cpp

+-----------------------+------------------------+----------------------------------+
| Control Plugin Name   |         Creator        |       Description                |
+=======================+========================+==================================+
| `Pipeline Sequence`_  | Carl Delsey            | A variant of a sequence node that|
|                       |                        | will re-tick previous children   |
|                       |                        | even if another child is running |
+-----------------------+------------------------+----------------------------------+
| `Recovery`_           | Carl Delsey            | Node must contain 2 children     |
|                       |                        | and returns success if first     |
|                       |                        | succeeds. If first fails, the    |
|                       |                        | second will be ticked. If        |
|                       |                        | successful, it will retry the    |
|                       |                        | first and then return its value  |
+-----------------------+------------------------+----------------------------------+
| `Round Robin`_        | Mohammad Haghighipanah | Will tick ``i`` th child until   |
|                       |                        | a result and move on to ``i+1``  |
+-----------------------+------------------------+----------------------------------+

.. _Pipeline Sequence: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/control/pipeline_sequence.cpp
.. _Recovery: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/control/recovery_node.cpp
.. _Round Robin: https://github.com/ros-planning/navigation2/tree/main/nav2_behavior_tree/plugins/control/round_robin_node.cpp
