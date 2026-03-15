---
title: "SE1. Use record-and-playback when performing exploratory field tests"
permalink: /guidelines/guideline-se1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> In order to effectively select which test scenarios should be escalated to the field, the testing teams often perform exploratory field tests [1]. Exploratory testing is an experience-based technique where the tester designs and executes tests based on prior knowledge, previous tests, curiosity, and other heuristics for common failures [2]. For instance, exploratory field tests may be useful for identifying corner cases that could be missed during design [3], or calibrating (e.g., tuning parameters [4, 5]) the system under scrutiny before committing to the field test scenario. ROS practitioners typically use Record and Playback (aka record-and-replay) for testing, debugging and developing new algorithms [6]. Record-and-playback is especially useful for performing exploratory tests of feedback loop systems since they provide lightweight means to record execution traces without preventing the testing team from freely exploring scenarios in the field. In ROS, record-and-playback is a technique that consists of recording message exchange between ROS nodes and enabling the user to reproduce the set of recorded messages in a specific order. The nominal use of record-and-playback, however, does not necessarily consider information from the field, placing the assessment (i.e., testing, debugging, analysis) in jeopardy.

## Reason (WHY)

Escalating exploration scenarios to the field asks for lightweight means to recording data for scenario reproduction.

## Suggestion (WHAT)

When running exploratory field testing, the QA team should use record-and-playback in order to keep track of the explored field scenarios, simplify error analysis, find and reproduce corner cases, and help with parameter tuning. The standard tool for record-and-playback in ROS is rosbag (wiki:[rosbag](http://wiki.ros.org/rosbag)) but there are a few tool derivations supporting effective record-and-playback. For example, Rerun.io (git:[rerun-io/rerun](https://github.com/rerun-io/rerun)) promotes a graphical interface with a focus on the visualization of bag data leveraging common datatypes used on perception algorithms. In addition, NuBots (git:[NUbots/NUbots](https://github.com/NUbots/NUbots)) uses a genetic algorithm for tuning parameters for the RoboCup over data collected in field explorations after data bags.

## Process (HOW)

Record-and-playback is well known by the ROS community. The ROS environment provides rosbag, a package that natively enables record-and-replay, which is frequently maintained and active. A few tools extend rosbags with addons 1 to more expressive visualizations and data types (e.g., Rerun.io) or building on largely used behavior models (i.e., behavior trees) to replay robot behavior within mixed-reality scenarios [7]. Moreover, record-and-replay for exploring field testing scenarios used for simplifying error analysis [8], finding corner cases [3], and parameter tuning [5, 4].

## Exemplars

#### Technology enablers

The standard library for record-and-playback in ROS is rosbag[(rosbag)](https://github.com/ros/ros_comm/tree/noetic-devel/tools/rosbag). The rosbag package provides a means for recording exchanged messages in so-called bag files and reproducing the messages between components in release order. In addition, the package contains tools for analyzing, processing logs, and visualizing exchanged messages. Recent research, builds on top of rosbag to encode more expressive tooling for applying records and reproducing for testing purposes, for instance using behavior trees to replay robot behavior in mixed reality [7]. 

          Rerun.io[(Rerun)](https://github.com/rerun-io/rerun)provides a general-purpose tool with focus on visualization of bag data which leverages common datatypes used in perception stack for robotics applications. Rerun enables URDF scene plotting, with 2d and 3d transformations, camera, odometry and tf transforms (e.g., rerun/ros_node).[(ros_node example)](https://github.com/rerun-io/rerun/blob/main/examples/python/ros_node/main.py)

#### Simplifying error analysis

Beul M. et al. [8] extensively used bags to record the state of their unmanned aerial vehicle during field testing, keeping rosbag activated even in between experiments to avoid setting up overhead. Once the experiments are done, the authors filter and analyse the data using in-house tools including recording mission executions, editing traces and loading them for testing purposes. Finally, the authors claim that the toolset helped by simplifying the error analysis that was running over exploratory field scenarios (named experiments) where they logged user-defined missions in terms of ordered sets of 4D waypoints.

#### Finding corner cases

Ortega A. et al. [3] studied field testing experiences with an industrial-strength service robot (i.e., for hospital disinfection) transitioning from lab experiments to an operational environment. They conclude that the field testing strategies employed can be categorized into two phases, exploratory field testing and field endurance tests. Exploratory field testing helps find defects caused by variability in the environment, thus identifying corner cases [3]. However, replicating corner cases is challenging due to a lack of tooling to extract data from the field experiments. After all, the data collected from the fields must be (re-)useable, asking for tooling such as record-and-replay.

#### Parameter tuning

Algorithms using multi-objective optimization for improving functionality [5] or managing quality attributes (e.g., reliability) at runtime [4] may benefit from recording data in exploration scenarios and playback for tuning parameters. Zahn b. et al. [5] implements NUbots and uses a genetic algorithm (namely NSGA-II) to tune the parameters of a kicking strategy for a football robot player in the Robocup, for that, they rely on record-andplayback. NUbots[(Nubots)](https://github.com/NUbots/NUbots), however, instead of relying on standard ROS tooling to 2 record-and-playback provide their own implementation. Similarly, Caldas et. al [4] uses an implementation of their own to record whether a healthcare system (namely BSN [9]) presents faults at task-level execution, then playback the recorded data in a data mining pipeline (using also NSGA-II) to tuning the parameters of a software controller.

Strengths:

Record-and-playback is a good instrument to reduce the need for maintenance during quality assurance. It fosters also the repeatability of scenarios that would be rather lost when exploring field scenarios in an ad hoc way.

Weaknesses:

Record-and-replay may not scale well [10], can be the door for security exploits [11], and lacks means for fine-grained control of their recording thus the emergence and need for extensions to rosbag.

References

> [1] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [2] S. Reid, “Software and systems engineering software testing part 1: Concepts and definitions,” ISO/IEC/IEEE 29119-1, Tech. Rep., 2013.
>
> [3] A. Ortega, N. Hochgeschwender et al., “Testing service robots in the field: An experience report,” in 2022 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE, 2022, pp. 165–172.
>
> [4] R. D. Caldas, A. Rodrigues et al., “A hybrid approach combining control theory and ai for engineering self-adaptive systems,” in Proceedings of the IEEE/ACM 15th International Symposium on Software Engineering for Adaptive and Self-Managing Systems, 2020, pp. 9–19.
>
> [5] B. Zahn, J. Fountain et al., “Optimization of robot movements using genetic algorithms and simulation,” in RoboCup 2019: Robot World Cup XXIII 23. Springer, 2019, pp. 466–475.
>
> [6] A. Afzal, C. Le Goues et al., “A study on challenges of testing robotic systems,” in 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020, pp. 96–107.
>
> [7] Z. Han, T. Williams et al., “Mixed-reality robot behavior replay: A system implementation,” arXiv preprint arXiv:2210.00075, 2022. 3
>
> [8] M. Beul, N. Krombach et al., “Autonomous navigation in a warehouse with a cognitive micro aerial vehicle,” in Robot Operating System (ROS). Springer, 2017, pp. 487–524.
>
> [9] E. B. Gil, R. Caldas et al., “Body sensor network: A self-adaptive system exemplar in the healthcare domain,” in 2021 International Symposium on Software Engineering for Adaptive and Self-Managing Systems (SEAMS). IEEE, 2021, pp. 224–230.
>
> [10] Y. Koo and S. Kim, “Distributed logging system for ros-based systems,” in 2019 IEEE International Conference on Big Data and Smart Computing (BigComp). IEEE, 2019, pp. 1–3.
>
> [11] S.-Y. Jeong, I.-J. Choi et al., “A study on ros vulnerabilities and countermeasure,” in Proceedings of the Companion of the 2017 ACM/IEEE International Conference on Human-Robot Interaction, 2017, pp. 147–148.
---------------------------------- GUIDELINE CONTENT END ----------------------------------
