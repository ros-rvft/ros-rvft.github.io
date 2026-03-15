---
title: "SDB2. Use Domain Specific Languages to Specify Properties"
permalink: /guidelines/guideline-sdb2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> To address the safety challenge, one option is defining a clearly specified and isolated layer, which is declared separately from the main program and that can express the functional safety-critical concerns in terms of externally observable properties of the software [1]. This guideline discusses the use of a Domain Specific Language to define the properties of the system.

## Reason (WHY)

As a more informal, code-like alternative, the QA team has the choice of utilizing a Runtime Verification tool that has a built-in ROS-tailored language and allows the quality assurance team to specify and validate the correct behaviour of the system.

## Suggestion (WHAT)

In complement to logic-based instruments, the QA team may opt to use verification tools that allow code-like specifications of properties to simplify the definition of the desired behavior. For example, ROSMonitoring (git:[autonomy-and-verification-uol/ROSMonitoring](https://github.com/autonomy-and-verification-uol/ROSMonitoring)) allows for code-like specifications of properties in a domain specific language (DSL) targeted to the properties such as writing assertions over the robot's position using if-else constructs.

## Process (HOW)

The works in [1, 2, 3] describe DSLs for specifying properties. The properties described with the DSL are checked mainly by intercepting the messages from relevant services and topics from the ROS system. It is important to consider the nature of the properties that should be specified and the expressiveness of the DSL. These DSLs give often the possibility to specify actions that should be performed in reaction to a violation of a safety property. It is important that the QA team chooses, customizes or conceives the DSL that best suits the specific needs.

## Exemplars

The runtime verification tools described in [2, 3] are based on a DSL that allows collecting the information from the different software components (ROS nodes) at a given moment in time and perform a corresponding action if one or more of the predefined rules are broken. In [3], the authors define ROSRV. Listing 1 shows the definition of a condition for which the system will be monitoring and the corresponding action to be taken in case a violation occurs.

Listing 1: Example of position and velocity property specification in ROSRV

```
1 event moveOrStop(double lx, double ly, double lz) 
          2 /landshark_control/base_velocity 
          3 geometry_msgs/TwistStamped 
          4 ’{twist:{linear:{x:lx,y:ly,z:lz}}}’ 
          5 { 
          6 if( posx > 9 ) { 
          7 if(vectory * lx < 0) { 
          8 ROS_WARN("Position not allowed"); 
          9 return; 
          10 } 
          11 } 
          12 }
```

#### ROSRV and RuBaSS

In ROSRV, the event definition structure is as follows. First, the keyword event must be followed by the event name and the parameters that need to be provided to the method. Consequently, one must state the topic name, data type and the mapping from the topic information to the method parameters. Such structure is shown in Listing 1. In [1], the property definition DSL (namely RuBaSS) allows incorporating time into the rule definition. For example, one can describe a safety property as "max speed exceeded: linear speed > max speed for 2 sec;" where the linear speed and max speed values are extracted from messages published in corresponding topics. Consequently, this property checks whether the comparison holds true for 2 seconds using the DSL defined by the authors.

Strengths:

The use of Domain Specific Languages for specifying properties brings a programmer-friendly interface for runtime validation. Moreover, it promotes the definition of well-structured and standardized approaches.

Weaknesses:

On the negative side, the expressiveness of properties is limited by the DSL used.

References

> [1] S. Adam, M. Larsen et al., “Rule-based dynamic safety monitoring for mobile robots,” Journal of Software Engineering for Robotics, vol. 7, no. 1, pp. 120–141, 2016.
>
> [2] A. Ferrando, R. C. Cardoso et al., “Rosmonitoring: a runtime verification framework for ros,” in Annual Conference Towards Autonomous Robotic Systems. Springer, 2020, pp. 387–399. 2
>
> [3] J. Huang, C. Erdogan et al., “Rosrv: Runtime verification for robots,” in International Conference on Runtime Verification. Springer, 2014, pp. 247–254.
---------------------------------- GUIDELINE CONTENT END ----------------------------------
