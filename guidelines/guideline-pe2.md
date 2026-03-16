---
title: "PE2. Create models for runtime assessment"
permalink: /guidelines/guideline-pe2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [model-based-testing, formal-verification, digital-twin, qa-team]
---

## Context (WHEN)

> Gaining confidence in the running systems can be costly due to the need for isolation from side effects, preservation of security and safety, controllability, and observability [1]. One way to address this issue is through the use of model-based runtime assessment, which can help to manage complexity and ensure the safe operation of ROS-based applications [2]. Models can be used to define safety criteria, create digital twins of the system and its environment, and ensure adequate test coverage. This guideline discusses creating models for managing the complexity of runtime assessment in ROS.

## Reason (WHY)

Modeling is essential for efficient and effective testing of ROS-based systems in the field. ROS-based systems lack a built-in system representation, making it difficult to identify and address bugs without costly calibration of sensors and actuators [3, 4, 5]. By incorporating models, such as those used in low-fidelity simulation, the testers can reveal the same bugs found in real-world navigation [6]. Implementing models in runtime assessment of ROS-based systems can save costs and improve the overall performance of the tests.

## Suggestion (WHAT)

The QA team might create and exploit models of the system and/or of its environment (a sort of digital twin) for runtime assessment, predictive maintenance, checking alternatives, and so on. For example, they can create a digital twin of the system by using CPSAML ([me-big-tuwien-ac-at/cpsaml](https://github.com/me-big-tuwien-ac-at)), or formal tools such as UPPAAL combined with UPPAALTron (doi:[10.1109/ECMR.2015.7324210](https://ieeexplore.ieee.org/document/7324210)). In addition, the QA team may use ROS metamodels ([ipa-nhg/ros-model](https://github.com/ipa320/RosTooling)) to facilitate the use of tools and graphical plug-ins for reverse engineering models from ROS code.

## Process (HOW)

Models can be used to create useful representations of the system’s components for runtime assessment of ROS-based applications, such representations include (i) models of the system itself, (ii) models of the environment and (iii) metamodels.(i) Models of the system itself consider digital twins of the system or part of the system [7, 8]. (ii) Models of the environment may be carried out in tools for formal verification, e.g., UPPAAL [9, 10]. (iii) Metamodels rely on the Eclipse Ecore technology to encoding rules for modeling, generating and introspecting ROS-based systems [11, 12]

## Exemplars

#### Models of the system itself

Saavedra Sueldo C. et al. [7] proposes an architecture for integrating digital twins (DTs) on production systems using ROS. The paper argues that digital twins should be used as the central component for the formulation of autonomous decision-making systems due to their static nature. In order to do this, in their online repository[INTELYMEC/ROS Tecnomatix](https://github.com/INTELYMEC/ROS_Tecnomatix)the authors provide a ROS node (named plant simulation node) that performs the same operations (e.g., decision using a method of reinforcement learning and a material handling procedure) of its counter-part, but in a controlled environment. The simulation node can be understood as a mock or model of self. In a similar direction, Fend A. and Bork D. [8] suggest model-driven runtime monitoring based on digital twins for ROS-based applications, namely CPSAML[(CPSA_ML)](https://github.com/me-big-tuwien-ac-at/cpsaml). CPSAML generates local DT components that are executed as ROS nodes. The DT component holds the state of the DT entity; in other words, it provides a model of the execution life-cycle of its counterpart. Ultimately, the model of the system can be used for reasoning during testing and runtime verification.

#### Models of the environment

The test setup described in Ernits et al. [9] uses UPPAAL Tron [10] as the primary test execution engine. First, the QA team should model, in UPPAAL, (i) an implementation model of the system under test and (ii) a topological map of the environment. Second, the QA team integrates an adapter, provided by Ernits et al. [9], which is responsible for translating messages between the environment model and the appropriate topics in ROS, acting as the interface between the ROS-based system under test and the UPPAAL Tron model of the environment. Finally, the interaction between the implementation model (i) and the environment model (ii) is monitored during system execution and afterwards, the equivalence between the measured outcomes from the running system and the outcomes from the model is checked. The operating environment, however, is typically prone to uncertainty which makes modeling the environment a costly activity.

Building on the use of UPPAAL for ROS verification, Dust et al. [13, 14] propose a pattern-based approach with reusable timed automata templates that model the execution behavior of ROS 2 nodes, including callback scheduling, buffer overflow, and end-to-end latency in processing chains. The approach supports both single-threaded and multi-threaded executors and has been validated against real ROS 2 execution traces. A model-based methodology further automates the process [15]: system parameters are extracted from ROS 2 execution traces generated by the ROS2\_tracing tool, then transformed through Eclipse Ecore metamodels into initialized UPPAAL formal model templates via model-to-model and model-to-text transformations, reducing the manual effort and domain expertise previously required for formal model construction.

#### Metamodels

One of the most notable works using models as a foundation for software development with ROS is the series on Bootstrapping MDE Development from ROS Manual Code [11, 12] by Hammoudeh Garcia N. In the repository[(ros-model)](https://github.com/ipa-nhg/ros-model), a set of metamodels defined as Ecore models are provided to facilitate the use of tools and graphical plug-ins for creating models from ROS code, composing and validating model compositions, auto generating deployment artifacts, and checking the use of standard specifications. The repository also includes tutorials on reverse engineering from ROS code to models, creating a model using introspection at runtime, and generating ROS code from models.

Strengths:

By using models for field-based testing, it is possible to reveal bugs in a safe and cost-effective way, without the need for costly and risky test campaigns in the field; It also allows for flexibly choosing the model representation, and the level of detail of the model, according to the needs of the system, the test scenarios, and the available resources. Models can be reused in different testing scenarios, and across different system components, reducing the effort and time required for testing.

Weaknesses:

Large and complex robotics systems may impair the creation and maintenance of runtime models. Models need to be updated and maintained as the system evolves, which can be a costly and time-consuming task. In addition, modeling can be prone to errors and inaccuracies, which can affect the quality of the testing results. Models are domain dependent and may not be easily transferrable between domains such as healthcare domain, automotive, or aerial domains.

References

> [1] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [2] C. Schlegel, T. Haßler et al., “Robotic software systems: From code-driven to model-driven designs,” in 2009 International Conference on Advanced Robotics. IEEE, 2009, pp. 1–8.
>
> [3] J. C. Kirchhof, J. Michael et al., “Model-driven digital twin construction: synthesizing the integration of cyber-physical systems with their information systems,” in Proceedings of the 23rd ACM/IEEE International Conference on Model Driven Engineering Languages and Systems, 2020, pp. 90–101.
>
> [4] E. Guerrero, F. Bonin-Font et al., “Adaptive visual information gathering for autonomous exploration of underwater environments,” IEEE Access, vol. 9, pp. 136 487–136 506, 2021.
>
> [5] T. Lewis and K. Bhaganagar, “Configurable simulation strategies for testing pollutant plume source localization algorithms using autonomous multisensor mobile robots,” International Journal of Advanced Robotic Systems, vol. 19, no. 2, p. 17298806221081325, 2022.
>
> [6] T. Sotiropoulos, H. Waeselynck et al., “Can robot navigation bugs be found in simulation? an exploratory study,” in 2017 IEEE International conference on software quality, reliability and security (QRS). IEEE, 2017, pp. 150–159.
>
> [7] C. Saavedra Sueldo, I. Perez Colo et al., “Ros-based architecture for fast digital twin development of smart manufacturing robotized systems,” Annals of Operations Research, pp. 1–25, 2022. 1Added after follow-up questionnaire on April 14th. 3
>
> [8] A. Fend and D. Bork, “Cpsaml: a language and code generation framework for digital twin based monitoring of mobile cyber-physical systems,” in Proceedings of the 25th International Conference on Model Driven Engineering Languages and Systems: Companion Proceedings, 2022, pp. 649–658.
>
> [9] J. Ernits, E. Halling et al., “Model-based integration testing of ros packages: A mobile robot case study,” in 2015 European Conference on Mobile Robots (ECMR). IEEE, 2015, pp. 1–7.
>
> [10] K. G. Larsen, M. Mikucionis et al., “Testing real-time embedded software using uppaal-tron: an industrial case study,” in Proceedings of the 5th ACM international conference on Embedded software, 2005, pp. 299–306.
>
> [11] N. Hammoudeh Garcia, M. L¨udtke et al., “Bootstrapping mde development from ros manual code - part 1: Metamodeling,” in 2019 Third IEEE International Conference on Robotic Computing (IRC), 2019, pp. 329–336.
>
> [12] N. Hammoudeh Garc´ıa, H. Deshpande et al., “Bootstrapping mde development from ros manual code: Part 2—model generation and leveraging models at runtime,” Software and Systems Modeling, vol. 20, no. 6, pp. 2047–2070, 2021.
>
> [13] L. Dust, R. Gu, C. Seceleanu, M. Ekström, and S. Mubeen, “Pattern-Based Verification of ROS 2 Nodes Using UPPAAL,” in Formal Methods for Industrial Critical Systems (FMICS), Lecture Notes in Computer Science, vol. 14290, Springer, 2023, pp. 57–75.
>
> [14] L. Dust, R. Gu, C. Seceleanu, M. Ekström, and S. Mubeen, “Pattern-based verification of ROS 2 applications using UPPAAL,” International Journal on Software Tools for Technology Transfer (STTT), vol. 27, pp. 313–332, 2025.
>
> [15] L. Dust, R. Gu, S. Mubeen, M. Ekström, and C. Seceleanu, “A model-based approach to automation of formal verification of ROS 2-based systems,” Frontiers in Robotics and AI, vol. 12, 2025.
