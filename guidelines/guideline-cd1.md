---
title: "CD1. Developers should strive for ROS nodes with single responsibility"
permalink: /guidelines/guideline-cd1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> ROS fosters a rich toolkit for designing modular robotics software [1]. Developers face design decisions of how to implement a given set of requirements using ROS fundamental concepts, i.e., nodes, topics, services, packages [2]. In order to facilitate runtime assessment, the system’s computational units should be designed such that they can be safely exposed to trials with warrantied no side effects on the running system [3]. In addition, it should reduce the cost of observing and controlling modules, or, in robotics, atomic actions (or skills) [4].

## Reason (WHY)

Mapping functional units to ROS nodes enables fine-grained observation and control of the robotic behavior.

## Suggestion (WHAT)

To facilitate assessment during the robot operation and enable fine-grained observation and control, the developers should implement ROS nodes following the single responsibility principle (i.e., each node should implement a single feature and different nodes can be combined to perform a complex task). For example, developers should implement independent nodes for path planning and reactive manoeuvring, or independent nodes for defining primitive skills like grasping an object or simultaneous localization and mapping (SLAM).

## Process (HOW)

We divide the means to designing ROS nodes with single responsibility in two: hierarchical design, and skill-based design. In hierarchical design, ROS nodes are organized based on the goals they achieve, with each node responsible for a specific task or functionality[5, 6]. This approach allows for clear separation of responsibilities and easier maintenance. In skill-based design, ROS nodes are organized based on the skills they possess, with each node responsible for a specific capability or behavior[7, 8, 9]. This approach enables more flexibility and reusability of nodes, as they can be combined to perform various tasks.

## Exemplars

#### Hierarchical design

Hierarchical design. Hartswell et al. define components as building blocks that may be hierarchically composed to fulfill the system’s functional requirements [5]. Their running example implements ROS nodes with complementary but distinct, 1 and independent, functionalities. One node resolves path planning in a deliberative control setting, and the other is responsible for the low-level PID controller reactively manoeuvring the robot.

In the healthcare domain, the Body Sensor Network (git:[lesunb/bsn](https://github.com/lesunb/bsn)) defines ROS nodes after concrete tasks that, composed, should fulfill the system’s goal. Tasks such as collecting SPO2 data, collecting heartbeat data, fuse data, or identifying emergency [6]. For instance, the[collect SPO2 data task](https://github.com/lesunb/bsn/blob/master/src/sa-bsn/target_system/components/component/src/g3t1_1/G3T1_1.cpp)implements an independent node for collecting, filtering, and transferring data. Given that each sub-task (i.e., collecting, filtering, and transferring) is strictly dependent on each other, yet, should not depend in the environment and together form an atomic behavior. Separating the sub-tasks in different nodes may render incomplete test cases that are hard to read and often meaningless.

#### Skill-based design

Skill-based design typically defines skills as fundamental software building blocks operating a modification on the world stage. In such approaches, skills should be modular and reusable. Although ROS nodes provide a natural means for modular design, it is not common to map skills to nodes in current skill-based designs. For instance, SkiROS [7] implements 3 nodes: World Model Manager, Task Manager, Skill Manager (i.e.,[skill manager](https://github.com/RVMI/skiros2/blob/de00abafffe78c8da6ba35e8259d6ad075ec72b6/skiros2_skill/src/skiros2_skill/core/skill.py#L622)).

In addition, HRMS [8] does not map skills to nodes. It builds skills that under the Behavior Trees notation may reuse existing[nodes](https://github.com/Gastd/py_trees_ros_behaviors/tree/devel/py_trees_ros_behaviors). Lack of standard mapping from skills to actual computation impairs the verification of skill-based approaches at skill level. Towards verifiable ROS-based applications, a promising architecture, namely[RobMoSys](https://robmosys.eu/wiki/general_principles:separation_of_levels_and_separation_of_concern), suggests separation of concerns between different levels such as Mission, Task Plot, Skill, Service, Function, whereas Skill concerns to configuration, e.g., grasp object with constraint, and functions concern to computation, e.g. inverse kinematics solver. In this direction, Albore A. et al. [9] promote ROS2 code generation whilst mapping skillsets to ROS nodes with a single responsibility.

Strengths:

Modularity enables fine-grained observation of system requirements. In addition, it caters to clear interfaces for runtime inspection and allows for mocking and substituting behavior for assurance scenarios.

Weaknesses:

Feedback loops, however, may impair testing, i.e., modularity turns out to be costly for systems with feedback loops, whereas the system’s behavior is context-dependent [10].

References

> [1] S. Limsoonthrakul, M. N. Dailey et al., “A modular system architecture for autonomous robots based on blackboard and  publish-subscribe mechanisms,” in 2008 IEEE International conference on robotics and biomimetics. IEEE, 2009, pp. 633–638.
>
> [2] I. Malavolta, G. A. Lewis et al., “Mining guidelines for architecting robotics software,” Journal of Systems and Software, vol. 178, p. 110969, 2021.
>
> [3] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [4] M. Efatmaneshnik and M. Ryan, “A study of the relationship between system testability and modularity,” INSIGHT, vol. 20, no. 1, pp. 20–24, 2017.
>
> [5] C. Hartsell, N. Mahadevan et al., “Model-based design for cps with learning-enabled components,” in Proceedings of the Workshop on Design Automation for CPS and IoT, 2019, pp. 1–9.
>
> [6] E. B. Gil, R. Caldas et al., “Body sensor network: A self-adaptive system exemplar in the healthcare domain,” in 2021 International Symposium on Software Engineering for Adaptive and Self-Managing Systems (SEAMS). IEEE, 2021, pp. 224–230.
>
> [7] F. Rovida, M. Crosby et al., “Skiros—a skill-based robot control platform on top of ros,” Robot Operating System (ROS) The Complete Reference (Volume 2), pp. 121–160, 2017.
>
> [8] G. Rodrigues, R. Caldas et al., “An architecture for mission coordination of heterogeneous robots,” Journal of Systems and Software, vol. 191, p. 111363, 2022.
>
> [9] A. Albore, D. Doose et al., “Skill-based design of dependable robotic architectures,” Robotics and Autonomous Systems, vol. 160, p. 104318, 2023.
>
> [10] C. Hutchison, M. Zizyte et al., “Robustness testing of autonomy software,” in 2018 IEEE/ACM 40th International Conference on Software Engineering: Software Engineering in Practice Track (ICSE-SEIP). IEEE, 2018, pp. 276–285.
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
