---
title: "I1. Provide an API for querying and updating internal lifecycle"
permalink: /guidelines/guideline-i1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [lifecycle, instrumentation, developer, ros2]
---

## Context (WHEN)

> Autonomous systems, such as robotic applications, often require stateful compute nodes [1]. However, the internal states within ROS nodes are typically hidden and not easily accessible, limiting the ability to diagnose and understand unexpected behavior. Exposing these hidden states is crucial for providing granular information on the system’s behavior, rendering increased observability. Furthermore, managing these hidden states allows for actions such as starting, stopping, and rolling back to a specific state, in other words, increased controllability. The running system should be both observable and controllable [2, 3], as these states can be application-specific and not standard [4].

## Reason (WHY)

The use of ROS nodes with lifecycle management can facilitate testing by providing a structured way to manage the state of the nodes and the interactions between them. This structure helps to ensure that nodes are in the right state for testing and that the interactions between nodes are predictable. Furthermore, it helps mitigate dangling references to nodes that are no longer in use

## Suggestion (WHAT)

To facilitate field-based testing, the development team should properly manage the ROS nodes’ lifecycle and prepare APIs for querying and updating the internal nodes’ life-cycle, e.g., to ensure that nodes are in the right state for testing. For example, developers can use modes (git:[ros2/demos](https://github.com/ros2/demos)) for lifecycle management. In the context of Micro-ROS (git:[micro-ROS](https://github.com/micro-ROS/)), developers can define custom lifecycle modes (git:[micro-ROS/system modes](https://github.com/micro-ROS/system_modes)) like sleep, power saving, starting, processing, and ending modes, and use separate extra nodes for mode monitoring and mode update.

## Process (HOW)

The team should define a custom life-cycle for the ROS-based application, for instance, the life-cycle phases could be: starting, processing, and ending [5], using system modes from Micro-ROS[6]. Moreover, the processing phase can further be divided into waiting and executing steps and application-specific states, and the transitions between phases should be well-defined by events. The development team should then prepare an API for managing the life-cycle of nodes [7], which can be queried or updated through ROS interfaces, such as the client-server interface. The API should allow for the representation of all nodes in the application, which can be queried or updated using the interface.

## Exemplars

#### Customized life-cycle

Customized life-cycle Conte G. et al. [5] define a custom life-cycle in ROS for their autonomous surface vehicle. The life cycle has three phases: starting, processing, and ending. The processing phase can be subdivided into two other: waiting and executing. Events define the transition between phases. The authors claim that such organization helped in the field testing when they had to explicitly shut down a (ROS) agent, shut down the agency infrastructure, or detect a failure in the ROS infrastructure. ROS2 provides the concept of life-cycle by design. Developers may inherit from the LifecycleNode from rclcpp to enable the standardized life-cycle management from ROS2. Belsare K. et al. [6], namely Micro-ROS , extends the ROS2 life-cycle to the domain of embedded systems. Their extension enables the specification of (sub-)systems or systems-of-systems in a hierarchical finite-state machine style. It creates the concept of modes within the active state. System modes are customizable and can be used to track sleep modes and power saving [7]. The authors present an example ([micro-ROS/system_modes/system_modes_examples](https://github.com/micro-ROS/system_modes/tree/master/system_modes_examples)) of how can add weak and strong as customized modes for an active manipulator.

Listing 1: YAML definition of custom system modes weak and strong for torque control.

> ```
> 1. manipulator: 
> 2. ros__parameters: 
> 3. type: node 
> 4. modes: 
> 5. __DEFAULT__: 
> 6. ros__parameters: 
> 7. max_torque: 0.1 
> 8. WEAK: 
> 9. ros__parameters: 
> 10. max_torque: 0.1 
> 11. STRONG: 
> 12. ros__parameters: 
> 13. max_torque: 0.2
> ```

#### Life-cycle management

Life-cycle management is the ability to query and update the nodes’ lifecycle.[rclc_lifecycle](https://github.com/ros2/rclc/tree/master/rclc_lifecycle)the library used by ROS2 provides the functionalities to managing nodes using the ROS2 stack [8]. rclc_lifecycle implements a ROS node that represents all other ROS nodes within the application. The nodes encode finite state machines that can be queried or updated using the ROS service interface. The[lifecycle talker example](https://github.com/ros2/demos/blob/foxy/lifecycle/src/lifecycle_service_client.cpp)illustrates how the get state and change state services query or update the life-cycle. The ROS2 implementation, however, does not support hierarchical states. To mitigate the problem, Micro-ROS  defines two extra nodes, the mode monitor node and the mode manager node [7]. The mode monitor infers the state (i.e., mode) of 2 underlying nodes; The mode manager may use the (inferred) state to update modes of sub-systems, modes of nodes, and node parameters.

Strengths:

Following this guideline results in reliable and repeatable runtime assessment since the life-cycle manager can ensure that the application is in the desired state. Moreover, it is easier to setup and teardown testing harnesses since it would be possible to understand the current state of the application, avoiding interruptions in critical phases, and planning for start and stop in the appropriate time.

Weaknesses:

As a drawback, there will be overhead associated with meta-data for life-cycle management, and increasing the number of lines of code may impact the system's latency. Also, custom states may ask for larger models representing the possible life-cycle and management, incurring in cost of modeling and maintenance.

References

> [1] C. Hutchison, M. Zizyte et al., “Robustness testing of autonomy software,” in 2018 IEEE/ACM 40th International Conference on Software Engineering: Software Engineering in Practice Track (ICSE-SEIP). IEEE, 2018, pp. 276–285.
>
> [2] Y. Falcone, S. Krsti´c et al., “A taxonomy for classifying runtime verification tools,” International Journal on Software Tools for Technology Transfer, vol. 23, no. 2, pp. 255–284, 2021.
>
> [3] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [4] I. Malavolta, G. A. Lewis et al., “Mining guidelines for architecting robotics software,” Journal of Systems and Software, vol. 178, p. 110969, 2021.
>
> [5] G. Conte, D. Scaradozzi et al., “Development and experimental tests of a ros multi-agent structure for autonomous surface vehicles,” Journal of Intelligent & Robotic Systems, vol. 92, no. 3, pp. 705–718, 2018.
>
> [6] K. Belsare, A. C. Rodriguez et al., “Micro-ros,” in Robot Operating System (ROS) The Complete Reference (Volume 7). Springer, 2023, pp. 3–55.
> [7] A. Nordmann, R. Lange et al., “System modes-digestible system (re-) configuration for robotics,” in 2021 IEEE/ACM 3rd International Workshop on Robotics Software Engineering (RoSE). IEEE, 2021, pp. 19–24. 3
>
> [8] J. Staschulat, I. Lutkebohle et al., “The rclc executor: Domain-specific deterministic scheduling mechanisms for ros applications on microcontrollers: work-in-progress,” in 2020 International Conference on Embedded Software (EMSOFT). IEEE, 2020, pp. 18–19. 4
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
