---
title: "MTA1. Improve the robustness of the system by performing noise and fault injection"
permalink: /guidelines/guideline-mta1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> When testing a robotic system, the QA team needs to gain confidence that it will behave safely when faced with unexpected inputs [1]. Techniques such as Fault Injection (FI) and Noise Injection (NI) can aid the QA team in identifying weaknesses, evaluating the resilience of the system as well as measuring its performance under stress. The deliberate introduction of faults such as hardware failures, network interruptions, software errors and signal alterations, can help assess how well the system recovers from these issues. In addition, fault injection is the central tool of a technique called Fault Based Testing, in which the generated test cases address potential faults that can be foreseen at design time[2].

## Reason (WHY)

Testing techniques based on fault injection and noise injection aid in increasing the overall reliability of the system under testing.

## Suggestion (WHAT)

The QA team can use tools that generate noise or inject faults to gain confidence that a robotic system will behave safely when faced with unexpected situations. For instance, RoboFuzz (git:[sslab-gatech/RoboFuzz](https://github.com/sslab-gatech/RoboFuzz)) enables the generation of faults (in ROS 2 applications) through message mutation with three intents: violation of physical laws, violation of user-specified properties, and cyber-physical discrepancies. Moreover, RosPenTo (git:[jr-robotics/ROSPenTo](https://github.com/jr-robotics/ROSPenTo)) enables security assessment by (un-) registering publishers or subscribers, isolating nodes or services, and injecting false data in the messages in ROS 1 applications.

## Process (HOW)

Fault injection is a testing technique to evaluate the robustness of a system that consists of intentionally introducing faults, failures and errors into the software system. The fault injection can occur at various levels, these generally are defined as the software, the hardware and the network layer. In the software layer, for instance, typical operations include the modification of variables and the manipulation of input data. Noise injection, instead, refers to introducing noise or interference into a system with the aim of improving the system’s resilience. Several tools have been developed in recent years to apply these concepts in the ROS domain, either based on noise injection ros1 fuzzer[(ros1_fuzzer)](https://github.com/aliasrobotics/ros1_fuzzer), ros2 fuzzer [3][(ros2_fuzzer)](https://github.com/aliasrobotics/ros2_fuzzer), or fault injection [4, 5] ROS Fault Injection Toolkit camfitool .

## Exemplars

#### Noise Injection

With the goal of effectively stressing a data-driven ROS system, Seulbae Kim et al. [3] implemented RoboFuzz[(RoboFuzz)](https://github.com/sslab-gatech/RoboFuzz), which is based on a data type-aware mutation technique aimed at finding correctness bugs in the system. RoboFuzz takes a target system and a test strategy as input and outputs the report of found bugs after performing a fuzzing technique based on message mutation. In addition, RosPenTo [6][(jr-robotics/ROSPenTo)](https://github.com/jr-robotics/ROSPenTo)provides the operations of unregistering and registering publishers/subscribers, isolating nodes and services, and injecting false data in messages. As an example, the authors show how to use the tool to isolate the safety monitor node and to inject fault data in a robotic operation in such a way that the robot may harm humans [6].

#### Fault Injection

Targeting the inclusion of Fault Injection in the system, the imfit  tool, which is based on applying mutation testing to relevant files with the ROS source code, is of great value [4]. The tool allows the user to create fault injection plans and select the operating conditions for the mutation process. Furthermore, fault metrics and diagrams can be obtained afterwards to analyze the system’s response. 
          
          In addition, ROS Fault Injection Toolkit is a tool that aims to test the reliability and fault-tolerance of a ROS-based system while allowing for usercontrolled fault injection, targeting especially the domain of image processing for autonomous driving. Similarly, camfitool[(camfitool)](http://wiki.ros.org/camfitool)is an official ROS tool which also allows the user to inject faults in images, but it additionally provides a simple intuitive graphical interface as well as the ability to perform the injection retrospectively or in real-time. In the domain of Unmanned Aerial Vehicles (UAV), the authors in [5] present a ROS-based application the system is built as a ROS node and leverages the ROS communication protocol and Linux system to inject faults. As an illustrating example, the authors analyse the effect of corrupting the execution of modules related to the generation of the flight command and measure the impact on the quality of flight. 1.6 Strengths It improves the reliability of the system. The faults injected can mirror real-world conditions. Demonstrating resilience can build confidence in the system. 1.7 Weaknesses Designing and implementing fault and(or) noise injection scenarios can be complex. Injected faults might lead to scenarios that never occur in the real world. The injection process can be resource-expensive and time-consuming. 2

Strengths:

It improves the reliability of the system. The faults injected can mirror real-world conditions. Demonstrating resilience can build confidence in the system.

Weaknesses:

Designing and implementing fault and(or) noise injection scenarios can be complex. Injected faults might lead to scenarios that never occur in the real world. The injection process can be resource-expensive and time-consuming.

> [1] C. Hutchison, M. Zizyte et al., “Robustness testing of autonomy software,” in 2018 IEEE/ACM 40th International Conference on Software Engineering: Software Engineering in Practice Track (ICSE-SEIP). IEEE, 2018, pp. 276–285.
>
> [2] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [3] S. Kim and T. Kim, “Robofuzz: Fuzzing robotic systems over robot operating system (ros) for finding correctness bugs,” in Proceedings of the 30th ACM Joint European Software Engineering Conference and Symposium on the Foundations of Software Engineering, ser. ESEC/FSE 2022. New York, NY, USA: Association for Computing Machinery, 2022, p. 447–458.
>
> [4] U. Yayan and C. Baglum, “Tailored mutation-based software fault injection tool (im-fit),” SoftwareX, p. 101463, 2023.
>
> [5] Y.-S. Hsiao, Z. Wan et al., “Mavfi: An end-to-end fault analysis framework with anomaly detection and recovery for micro aerial vehicles,” arXiv preprint arXiv:2105.12882, 2021.
>
> [6] B. Dieber, R. White et al., “Penetration testing ros,” Robot Operating System (ROS), p. 183, 2020. 3
---------------------------------- GUIDELINE CONTENT END ----------------------------------
