---
title: "SDB1. Property specification using a logic-based language"
permalink: /guidelines/guideline-sdb1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> Robotics systems are complex, inherently hybrid systems that combine hardware and software components and whose behaviour is often dictated by close safety, legal, and ethical considerations [1]. Furthermore, given the increasingly frequent deployment of ROS-based systems in safety-critical environments coupled with their dependence on complex decision-making and sophisticated control systems, it becomes necessary to find a form of verification that can reliably assess the correctness of these systems. This guideline discusses the use of formal and logic-based languages for specifying properties for runtime verification and/or field-based testing.

## Reason (WHY)

A logic-based language for verification and/or testing allows specifying properties that describe observable actions, outputs, how they relate to each other and when they should manifest [2]. The behaviour is often described using temporal logic, which enables the specification of desired or undesired interactions amongst multiple components (ROS nodes) regardless of the complexity of the system. To simplify the specification of properties in temporal logic, some of the tools refer to existent property specification patterns [3], i.e., a collection of existing known recurrent patterns for the specification of temporal properties. Specification patterns also enable the properties formulation in English thanks to a bidirectional mapping from various temporal logics to a structured English grammar.

## Suggestion (WHAT)

he QA team should be prepared to specify properties using unambiguous and precise languages like logic-based languages, as often required by verification tools. User-friendly instruments, like specification patterns (http:[ps-patterns](http://ps-patterns.wikidot.com/)), might facilitate the error-prone specification process and make the specification accessible to people lacking expertise in logic. For example, HAROS (git:[git-afsantos/haros](https://github.com/git-afsantos/haros)) uses a logic-based language called HPL for property specification that is used to synthesize runtime monitors for testing and verification.
## Process (HOW)

There are several choices of tools that use logic-based languages for properties specification [4, 5, 6, 7, 8]. These tools allow for safety, security, and liveness analyses. The formal specification languages for ROS-based systems should provide references to individual resources (e.g. topics) and message contents 1 as well as temporal operators and relations in addition to real-time behaviour specifications.

## Exemplars

#### Linear Temporal Logic (LTL)

The identified tools make use of various types of temporal logic. Linear Temporal Logic (LTL). The work in [8] proposes a novel architecture, for assertion-based verification by using monitors synthesized automatically from Linear Temporal Logic (LTL) assertions. Then, the monitors are encapsulated into plug-and-play ROS nodes and docker containerization is used to improve system portability. As an example, Listing 1 shows an LTL assertion to check if a robot arrives at a position $$ before a certain timeout.

Listing 1: LTL assertion to check if a robot reaches a desired position

```
1 always((robot x1 = x1 && robot y1 = y1 && newGoal) 
          2 implies 
          3 (currentTime < timeOut U robot x2 = x2 && robot y2 = y2))
```

#### Signal Temporal Logic (STL)

Signal-temporal logic is a special case of MTL where properties are defined over signals. They enable real-time reasoning and constraint specification. In [7, 9], Signal Temporal Logic (STL) is used to describe Cyber-Physical Systems (CPS) properties. The approach introduces the novel quality of robustness semantics, which implies the system’s ability to measure how far is an observed behaviour from satisfying or violating a specification. Concretely, the developed tool was rmtat , which was later augmented to support integration with ROS-based systems with rtamt4ros .

#### Metric Temporal Logic (MTL)

Some runtime verification tools add the ability to handle real-time specifications since the reaction time can have a strong influence on the success or failure of the robot’s mission. Taking this aspect into consideration, the RV tools described in [4, 6] use Metric Temporal Logic. On the other hand, [5] addresses it by combining Past-Time LTL to express complex formulas with timed constraints on the evaluation of these formulas. Hu et al. design their robot monitoring specification language based on Discrete Time-MTL (DT-MTL)s [6]. The language’s syntax embeds a time interval in the traditional MTL notation. Their approach uses the system’s periodic nature to discretize the real-time property and replace the real number in time constraints with the number of CPU clock cycles.

#### Timed Computational Tree Logic (TCTL)

Timed automata is one of the most widely used formal models to specify and verify real-time systems. Rodrigues A. et al. specify timing constraints using Timed Computational Tree Logic (TCTL) to encoding the requirements of a safety-critical healthcare monitoring system in ROSseams18/uppaal  [10]. Halder et al. specify UPPAAL models over ROS applications by performing manual code analysis. This phase requires the extraction of ROS code parameters that affect the desired properties of ROS-based robotic applications, including the publishing rate, the subscriber’s spin rate to process callbacks, the time to transmit messages over channels, and the time to process callbacks. Properties 2 are specified over queue overflow constraints [11].

#### Patterns-based specification

In [4], the authors introduce HAROS, which is a framework for quality assurance of ROS-based code. The use of the formal language HPL ensures that after entering a state of high priority (where the messages in the topic ’/state’ have data greater than 0), the system should remain in that state for, at least, one second. This can be accomplished through the following property definition: "globally: /state {data > 0} forbids /state {not data > 0} within 1000 ms". As can be seen, the property specification makes use of specification patterns, similar to the absence pattern with a time constraint [3]. Recently, other sets of patterns specific to robotics have been defined [12, 13]; even though they have been conceived for mission specification, they could be profitably used for verification and (scenario-based) testing.

#### Structured Natural Language with FRET

An alternative approach to specifying properties in logic is to use structured natural language that automatically translates to temporal logic. NASA's Formal Requirements Elicitation Tool (FRET) [14, 15] allows the QA team to write requirements in FRETISH, a restricted English language with precise, unambiguous semantics. For each requirement, FRET automatically generates formalizations in both future-time and past-time metric temporal logic. FRETISH requirements follow a structured template; for example, a safety requirement can be expressed as: "When in\_mission, the UAV shall always satisfy (current\_consumption &lt; max\_current)". FRET translates such requirements into temporal logic formulae that can be exported for use in analysis and monitor generation tools (see [MTA2](/guidelines/guideline-mta2) for the automated monitor generation pipeline). FRET v3.0 further supports probabilistic requirement specification and automated test case generation [16]. FRET has been applied to robotics domains with a dedicated focus on ROS 2 applications [17] and is open-source at [https://github.com/NASA-SW-VnV/fret](https://github.com/NASA-SW-VnV/fret).

Strengths:

Using logic-based languages to specifying properties offers a standardized approach to validation in compliance with well-adopted specification pattern.

Weaknesses:

It is noted that the properties' expressiveness is often limited by the description language meaning that diffent languages and tool sets may enable specific property specifications or not.

References

> [1] M. Luckcuck, M. Farrell et al., “Formal specification and verification of autonomous robotic systems: A survey,” ACM Computing Surveys (CSUR), vol. 52, no. 5, pp. 1–41, 2019.
>
> [2] A. F. F. Santos, “Safety verification for ros software,” Ph.D. dissertation, Universidade do Minho, 2021.
>
> [3] M. Autili, L. Grunske et al., “Aligning qualitative, real-time, and probabilistic property specification patterns using a structured english grammar,” IEEE Transactions on Software Engineering, vol. 41, no. 7, pp. 620–638, 2015.
>
> [4] A. Santos, A. Cunha et al., “The high-assurance ros framework,” in 2021 IEEE/ACM 3rd International Workshop on Robotics Software Engineering (RoSE). IEEE, 2021, pp. 37–40.
>
> [5] C. Lesire, S. Roussel et al., “Synthesis of real-time observers from pasttime linear temporal logic and timed specification,” in 2019
> International Conference on Robotics and Automation (ICRA), 2019, pp. 597–603. 3
>
> [6] C. Hu, W. Dong et al., “Runtime verification on hierarchical properties of ros-based robot swarms,” IEEE Transactions on Reliability, vol. 69, no. 2, pp. 674–689, 2019.
>
> [7] D. Niˇckovi´c and T. Yamaguchi, “Rtamt: Online robustness monitors from stl,” in International Symposium on Automated Technology for Verification and Analysis. Springer, 2020, pp. 564–571.
>
> [8] S. Aldegheri, N. Bombieri et al., “A containerized ros-compliant verification environment for robotic systems,” in 2021 Design, Automation & Test in Europe Conference & Exhibition (DATE). IEEE, 2021, pp. 222–225.
>
> [9] T. Yamaguchi, B. Hoxha et al., “Rtamt–runtime robustness monitors with application to cps and robotics,” International Journal on Software Tools for Technology Transfer, pp. 1–21, 2023.
>
> [10] A. Rodrigues, R. D. Caldas et al., “A learning approach to enhance assurances for real-time self-adaptive systems,” in 2018 IEEE/ACM 13th International Symposium on Software Engineering for Adaptive and Self- Managing Systems (SEAMS). IEEE, 2018, pp. 206–216.
>
> [11] R. Halder, J. Proen¸ca et al., “Formal verification of ros-based robotic applications using timed-automata,” in 2017 IEEE/ACM 5th International FME Workshop on Formal Methods in Software Engineering (FormaliSE). IEEE, 2017, pp. 44–50.
>
> [12] C. Menghi, C. Tsigkanos et al., “Specification patterns for robotic missions,” IEEE Transactions on Software Engineering, vol. 47, no. 10, pp. 2208–2224, oct 2021.
>
> [13] ——, “Mission specification patterns for mobile robots: Providing support for quantitative properties,” IEEE Trans. Softw. Eng., vol. 49, no. 4, p. 2741–2760, dec 2022.
>
> [14] D. Giannakopoulou, T. Pressburger, A. Mavridou, J. Rhein, J. Schumann, and N. Shi, “Formal Requirements Elicitation with FRET,” in Joint Proceedings of REFSQ-2020 Workshops, CEUR Workshop Proceedings, vol. 2584, 2020.
>
> [15] D. Giannakopoulou, T. Pressburger, A. Mavridou, and J. Schumann, “Automated formalization of structured natural language requirements,” Information and Software Technology, vol. 137, p. 106590, 2021.
>
> [16] A. Katis, A. Mavridou, D. Giannakopoulou, T. Pressburger, and J. Schumann, “Capture, Analyze, Diagnose: Realizability Checking of Requirements in FRET,” in Computer Aided Verification (CAV), LNCS, vol. 13372, Springer, 2022, pp. 484–495.
>
> [17] G. Vazquez, A. Mavridou, M. Farrell, T. Pressburger, and R. Calinescu, “Robotics: A New Mission for FRET Requirements,” in NASA Formal Methods (NFM), 2024.
