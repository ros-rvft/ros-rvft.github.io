---
title: "SDB3. Use languages and tools to scenario-based specification of test cases"
permalink: /guidelines/guideline-sdb3
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [scenario-testing, simulation, qa-team]
---

## Context (WHEN)

> Scenario specification allows the QA team to test robots on credible and complex activities since it defines the course of a robotic mission [1]. Gathering confidence in autonomous systems through so-called verified scenarios is a cornerstone of simulation testing [2]. However, designing test cases in the form of scenarios implicitly requires accounting for possible variations and conditions. This makes scenario-based testing a challenging task and often deemed infeasible. In addition, unexpected scenarios frequently underlie failures in robotic systems [1]. Therefore, it is important to consider real-world data during scenario generation since it permits to focus on a range of scenarios that can be unexpected during the design phase [3].

## Reason (WHY)

Scenario-based test case generation is a powerful approach to verify ROS-based applications because it allows for the systematic exploration of different situations and conditions that the robotic system may encounter in the real world. By defining scenarios, the testing team can ensure that the application behaves correctly under a wide range of circumstances, including both expected and unexpected events.

## Suggestion (WHAT)

The QA team might integrate scenario specification languages and tools to enable a systematic exploration of real-world situations and conditions for ROS-based applications. For example, Geoscenario (git:[rodrigoqueiroz/geoscenarioserver](https://github.com/rodrigoqueiroz/geoscenarioserver)) uses behavior trees to program dynamic interactions between the system-under-test and other vehicles in the scenario. In addition, SCENIC (git:[BerkeleyLearn-Verify/Scenic](https://github.com/BerkeleyLearnVerify/Scenic)) is a probability-based programming language that enables the specification of rare events in environment models that are used to generate test cases for vehicles running on the CARLA simulator (git:[carla-simulator/carla](https://github.com/carla-simulator/carla)) that may be further integrated to testing ROS-based systems.

## Process (HOW)

To implement scenario-based specifications for testing ROS-based applications we recommend describing technology enablers and motivating use cases. Technology enablers, in this case, list a set of languages that assist the design of scenarios for testing ROS-based applications. The technology-enablers vary with respect to human-vehicle behavioral description [4], to probability-based programming of scenarios [5], and integrating graphical simulation with Simulink-based control design and ROS [6]. From the point-of-view of use cases, scenario specification 1 may turn useful to perception monitoring [7], validating multi-layered control strategies [8], and pedestrian simulation scenarios [9].

## Exemplars

#### GeoScenario

GeoScenario [4] proposes using a behavior tree-based DSL to describe autonomous human-vehicle models for scenario-based testing. The toolset advocates for scenario specifications that reflect dynamic interactions between humans and the subject system in real traffic conditions. Therefore, behavior trees are used as a fundamental control-flow strategy. GeoScenario interfaces with a simulation layer where LIDAR and camera capture data from the vehicle controller implemented at ROS-level. Listing 1 showcases an implementation of one of the agent’s behavior in a pre-crash scenario from NHTSA. The vehicle changes the lane to the left, then continues driving using another drive tree implementation. The operator ’?’ stands for fallback operation, ’-’ is sequential, ’condition’ evaluates to a Boolean value, and ’maneuver’ executes a task.

Listing 1: Lane change human-vehicle implementation in Geoscenario.

```
1 behaviortree LaneChange: 
          2 ? 
          3 -> 
          4 condition c_trigger(sim_time (tmin=4)) 
          5 -> 
          6 condition c_reach(gap(target_lane=Left,range=5,repeat=False)) 
          7 maneuver cutin(MCutInConfig(target_lane=Left,delta_s=(5,-3,0))) 
          8 subtree drive_tree(m_vel_keep=MVelKeepConfig(vel=MP(14.0,10,6)))
```

#### SCENIC

SCENIC [5], a probability-based programming language, argues for the specification of rare events in environment models for autonomous vehicles and robots for testing purposes. The language relies on the specification of scenarios, i.e., configurations of physical objects and agents, and how they change over time. In combination with CARLA [10], SCENIC can be used to specify scenarios for ROS-based simulation test scenarios. For example, departing from a Metric Temporal Logic (MTL) safety specification, SCENIC generates (with VERIFAI [11]) 2000 scenarios for a vehicle performing a right turn at an intersection, yielding to the crossing traffic. Supporting Software-In-the-Loop (SIL) simulation testing, Xu C., et al. [6], introduces a platform that unites PreScan [12], MATLAB/Simulink [13], and ROS. The three-layered platform enables virtual sensors and scenarios designed in PreScan, control design in MATLAB/Simulink, and environment perception, planning and control execution at ROS-level. The proposed stack features graphical scenario specification including sensor simulation and may be used for mobile robotics with a focus on self-driving simulation testing.

Use Cases: The work in [7] integrates PerceMon , a tool for monitoring spatio-temporal specifications for perception systems, with the CARLA simulator 2 (integrated with ROS), and, in cohort with the OpenSCENARIO specification format defines a set of high-level scenarios for their experimentation setting. Their experimental scenario features sunlight exposure, cyclists crossing or poorly occluded pedestrians, and rendering corner case test fixtures. Similarly, [8] utilizes a ROS-CoppeliaSim [14] integration to validate their three-layered control decoupling strategy for lateral and longitudinal motion. The tool permits defining motion constraints to the mechanical joint points of the high-precision vehicle model, which forms a front-wheel steering and rear-wheel drive smart car model powered by Ackerman steering. [9] uses pedsim ros , a pedestrian simulator tool that relies on XML scene specification, for example Listing 2.

Listing 2: Corridor scenario specification with pedsim ros.

```
1 <?xml version="1.0" encoding="UTF-8"?> 
          2 <scenario> 
          3 <!--Obstacles--> 
          4 <obstacle x1="-0.5" y1="-0.5" x2="29.5" y2="-0.5"/> 
          5 <obstacle x1="-0.5" y1="-0.5" x2="-0.5" y2="14.5"/> 
          6 <obstacle x1="-0.5" y1="14.5" x2="29.5" y2="14.5"/> 
          7 <obstacle x1="29.5" y1="-0.5" x2="29.5" y2="14.5"/> 
          8 
          9 <waypoint id="east" x="5" y="5" r="2" b="1"/> 
          10 <!-- Sink --> 
          11 <waypoint id="west" x="25" y="5" r="2" b="2"/> 
          12 
          13 <waypoint id="robot_goal" x="22" y="27" r="2"/> 
          14 <waypoint id="robot_start" x="4" y="4" r="2"/> 
          15 
          16 <agent x="4" y="4" n="1" dx="0" dy="0" type="2"> 
          17 <addwaypoint id="robot_start"/> 
          18 <addwaypoint id="robot_goal"/> 
          19 </agent> 
          20 
          21 <!--AgentClusters--> 
          22 <source x="2" y="5" n="8" dx="3" dy="5" type="0"> 
          23 <addwaypoint id="east"/> 
          24 <addwaypoint id="west"/> 
          25 </source> 
          26 </scenario>
```

Strengths:

Scenario-based testing provides a systematic and comprehensive approach to verify ROS-based applications under various conditions. The integration of scenarios with ROS-compatible simulation environments allows for realistic and repeatable testing.

Weaknesses:

The exemplars provided are primarily focused on the automotive domain, which may limit the generalizability of the guideline to other robotic application domains.

References

> [1] A. Afzal, C. Le Goues et al., “A study on challenges of testing robotic systems,” in 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020, pp. 96–107.
>
> [2] M. Luckcuck, M. Farrell et al., “Formal specification and verification of autonomous robotic systems: A survey,” ACM Computing Surveys (CSUR), vol. 52, no. 5, pp. 1–41, 2019.
>
> [3] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [4] R. Queiroz, D. Sharma et al., “A driver-vehicle model for ads scenario-based testing,” arXiv preprint arXiv:2205.02911, 2022.
>
> [5] D. J. Fremont, E. Kim et al., “Scenic: A language for scenario specification and data generation,” Machine Learning, pp. 1–45, 2022.
>
> [6] C. Xu, H. Huang et al., “Sil simulation test platform based on prescan and ros,” in 2022 International Conference on Cyber-Physical Social Intelligence (ICCSI). IEEE, 2022, pp. 240–244.
>
> [7] A. Balakrishnan, J. Deshmukh et al., “Percemon: Online monitoring for perception systems,” in International Conference on Runtime Verification. Springer, 2021, pp. 297–308.
>
> [8] X. Duan, Q. Wang et al., “Implementing trajectory tracking control algorithm for autonomous vehicles,” in 2021 IEEE International Conference on Unmanned Systems (ICUS). IEEE, 2021, pp. 947–953.
>
> [9] S. B. Liu, H. Roehm et al., “Provably safe motion of mobile robots in human environments,” in 2017 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE, 2017, pp. 1351–1357.
>
> [10] A. Dosovitskiy, G. Ros et al., “Carla: An open urban driving simulator,” in Conference on robot learning. PMLR, 2017, pp. 1–16.
>
> [11] D. Tommaso, D. J. Fremont et al., “Verifai: A toolkit for the design and analysis of artificial intelligence-based systems,” in Proceedings of the 31st Conference on Computer Aided Verification, CAV 2019, 2019.
>
> [12] M. Tideman, “Scenario-based simulation environment for assistance systems,” ATZautotechnology, vol. 10, no. 1, pp. 28–32, 2010. 4
>
> [13] S. Documentation, “Simulation and model-based design,” 2020. [Online]. Available: https://www.mathworks.com/products/simulink.html
>
> [14] E. Rohmer, S. P. N. Singh et al., “V-rep: A versatile and scalable robot simulation framework,” in 2013 IEEE/RSJ International Conference on Intelligent Robots and Systems, 2013, pp. 1321–1326. 5
---------------------------------- GUIDELINE CONTENT END ----------------------------------
