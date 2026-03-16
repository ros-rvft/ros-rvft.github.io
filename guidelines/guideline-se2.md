---
title: "SE2. No GUIs! Prioritize headless simulation"
permalink: /guidelines/guideline-se2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [simulation, headless, qa-team]
---

## Context (WHEN)

> Simulation is a great way to validate that a robot behaves as expected [1]. It can also be used in hybrid approaches to combine real data from field with simulation engines, therefore making the testing more realistic [2]. Then, simulation can be useful as an isolation mechanism for testing, given that it can separate in-vivo testing from the production processes by reproducing the main process in a simulator based on information gather from the main execution by means of probes [3].
>
> Furthermore, as mentioned in [4], the QA team can use replay and subsystem testing to check the behaviour of certain components of the system without a full simulation by starting them up in isolation and replaying the logs. Running the simulators stripped of their Graphical User Interface (GUI), also referred to as headless simulation, allows QA teams to (i) scale up the testing of the robot behavior towards large-scale experimentation, (ii) reduce the resources consumption, and (iii) properly organize experiment with automatic generation of scenarios, operation environments where the robots should act, and/or automatic injection of noise or uncertainty.

## Reason (WHY)

Running the simulation headlessly allows one to avoid the overhead of rendering graphics and updating the GUI, as well as help in saving computational resources. Furthermore, headless simulation enables automation and make it feasible to integrate simulation with testing activities and incorporate it into continuous integration / continuous deployment (CI/CD) pipelines.

## Suggestion (WHAT)

When it is possible to test or verify without human supervision, the QA team should prioritize headless simulation to avoid unnecessary overhead, enable large-scale experimentation, and facilitate integration with CI/CD pipelines. Example of tools supporting headless simulation are Gazebo (git:[gazebosim/gz-sim](https://github.com/gazebosim/gz-sim)), V-REP (wiki:[V-REP](http://wiki.ros.org/vrep\_ros\_bridge)), ARGOS (http:[ARGOS](https://www.argos-sim.info/)), MORSE (git:[MORSE](https://morse-simulator.github.io/)), and MVSim (git:[MRPT/mvsim](https://github.com/MRPT/mvsim)). As a complement, OpenDaVINCI (git:[se-research/OpenDaVINCI](https://github.com/se-research/OpenDaVINCI)) interfaces with ROS and has been widely used for testing autonomous driving systems.

## Process (HOW)

To run a simulator in headless mode, the user typically needs to specify a particular command-line argument or configuration setting before initiating the simulation. Although, in most of these simulators, the visual interface and the simulation engine are tightly coupled [5], many of them, including Gazebo, V-REP, ArGoS [6, 7], MORSE, MVSim, and OpenDaVinci [8] allow for this setting to be set.

## Exemplars

#### Technology enablers

Most of the widely used simulators in the domain of robotics have a way to specify the intention of running the simulation headless. In Gazebo, it is done by specifying an option either through the command line or in the launch file1, although as stated in [5], there is still some instability in the support of this feature. V-REP also allows a user to set a headless simulation by adding a special option in the execution of the program.2 Furthermore, the ARGOS simulator [6], created to support the simulation of large scales swarms of robots, efficiently supports a headless mode of operation; it has been proven to outperform Gazebo and V-Rep simulators when running headless in small scenes with up to 10 robots [7].

Other simulators that allow headless operations include MORSE[(MORSE)](https://morse-simulator.github.io/), although the feature has only been tested in Linux, and MRPT/mvsim[(mvsim)](https://github.com/MRPT/mvsim), which is a lightweight simulator capable of running real-time scenarios for multiple vehicles.

Use cases: The authors of [5] propose a paradigm to incorporate validation via headless simulation into the continuous integration cycle. In addition to providing an illustrating use case of how to build and connect the different component of such a system, they provide a set of generic steps to be followed during the setup phase. The authors of [8] develop a system in which they setup a virtual test environment targeting algorithms that will run in complex autonomous driving systems. As a result of this work, they build the open source environment OpenDaVinci, which includes libraries that enable the reuse of the algorithms to be tested in headless simulations as part of unit tests. They demonstrate how to use the framework in combination with the simulation environment to develop a self-parking algorithm.

Strengths:

With headless simulation, the feedback is obtained faster, the simulations therefore can scale across multiple processors and cloud servers, and it makes possible to integrate the simulation into continuous integration pipelines.

Weaknesses:

Debugging is more challenging without visual feedback as it is considerably more difficult to locate the issues or understand unusual behavior.

References

> [1] A. Afzal, C. Le Goues et al., “A study on challenges of testing robotic systems,” in 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020, pp. 96–107.
>
> [2] C. Hildebrandt and S. Elbaum, “World-in-the-loop simulation for autonomous systems validation,” in 2021 IEEE International Conference on Robotics and Automation (ICRA). IEEE, 2021, pp. 10 912–10 919.
>
> [3] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [4]C. Hutchison, M. Zizyte et al., “Robustness testing of autonomy software,” in 2018 IEEE/ACM 40th International Conference on Software Engineering: Software Engineering in Practice Track (ICSE-SEIP). IEEE, 2018, pp. 276–285.
>
> [5] V. Estivill-Castro, R. Hexel et al., “Continuous integration for testing full robotic behaviours in a gui-stripped simulation.” in MoDELS (Workshops), 2018, pp. 453–464.
>
> [6] C. Pinciroli, V. Trianni et al., “ARGoS: a modular, parallel, multi-engine simulator for multi-robot systems,” Swarm Intelligence, vol. 6, no. 4, pp. 271–295, 2012.
>
> [7]  L. Pitonakova, M. Giuliani et al., “Feature and performance comparison of the v-rep, gazebo and argos robot simulators,” in Towards Autonomous Robotic Systems: 19th Annual Conference, TAROS 2018, Bristol, UK July 25-27, 2018, Proceedings 19. Springer, 2018, pp. 357–368.
>
> [8] C. Berger, “An open continuous deployment infrastructure for a self-driving vehicle ecosystem,” in Open Source Systems: Integrating Communities: 12th IFIP WG 2.13 International Conference, OSS 2016, Gothenburg, Sweden, May 30-June 2, 2016, Proceedings 12. Springer, 2016, pp. 177–183. 3
---------------------------------- GUIDELINE CONTENT END ----------------------------------
