---
title: "AR1. Perform postmortem analysis to diagnose non-passing test cases"
permalink: /guidelines/guideline-ar1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [diagnosis, postmortem, qa-team]
---

## Context (WHEN)

> The test case execution phase results in reports yielding a set of ran test cases  paired with Boolean results attesting whether the cases passed or failed. Failing  test cases, often, indicate the reason for failure by comparing the expected outcome  with the actual outcome. However, that may not be enough to understand  why did the robot fail that test case, since such assertions do not comprehensively  entail structural information about how the ROS-based system under test works.  Such lack of information poses a risk to the usefulness of the executed tests. In  order to provide fruitful information back to the development team, the testers  should make the most out of the data by delving into a postmortem analysis for  deriving explanations for the failed case [1].

## Reason (WHY)

The postmortem analysis is essential for understanding the reasons behind the  failure of test cases in ROS-based systems.

## Suggestion (WHAT)

The QA team should perform postmortem analysis and diagnose of non-passing  test cases to explain the failures to developers or refine the arguments and confidence  in the robotic system. For example, ROS projects may use a combination  of Nagios (web:[https://www.nagios.org/](https://www.nagios.org/)) and ros/diagnostics (web:[ros/diagnostics](http://wiki.ros.org/diagnostics)) for monitoring,  collecting and aggregating runtime data to diagnose failures. Moreover, CARE  (git:[softsys4ai/care](https://github.com/softsys4ai/care)) may be used for semi-automatic diagnosis of launch file misconfigurations  or may rely on approaches such as Rason (git:[lsa-pucrs/rason](https://github.com/lsa-pucrs/rason))  for multi-robot diagnosis.

## Process (HOW)

Natively, ROS provides a diagnostics infra, the ros/diagnostics package[(diagnostics)](http://wiki.ros.org/diagnostics), the  package enables manual data aggregation and analysis. However, unveiling  explanations for the test case failure requires better support. The testing team  may rely on visualization techniques [2], semi-automatic diagnostic generators [3,  4], and deployment of extra infrastructure to support explanations with more  data [5].

## Exemplars

#### Visualization

Often, roboticists need to use their technical experience to identify points of failure and diagnose failed test cases. With that in mind,  Roman F. et al. [2] propose Overseer, an architecture that unites Nagios (i.e., a  general-purpose open-source monitoring tool3) and ros/diagnostics (i.e., standard  tooling for collecting and aggregating runtime data in ROS) as a key-enabler  to visualization the runtime information and, in consequence, diagnostics. The  overseer implements a monitoring server responsible for persisting data generated  during the experiments in a database that can be later accessed by Nagios.

#### Semi-automated diagnosis

Causal Robotics DEbugging[(CARE)](https://github.com/softsys4ai/care)[3] is a  two-phase method for diagnosing configuration faults (aka misconfigurations) in  ROS-based systems. The method proposes first a causal model learning step,  then an inference over the learnt model step. The causal model is three-layered  and defines causal relations between (i) software-level configurations or hardwarelevel  options (e.g., sensors), (ii) a map from configuration options to how they  influence the outcome performance, and (iii) performance goals. The authors  employ Fast Causal Inference (FCI) to extract the causal model from data. Moreover,  the authors present an algorithm for causal path discovery (by inference)  which finds a locally optimal path between configuration (aka symptom) and performance  goal. Following a similar idea of three layered causal models, Kirchner  D. et al. implemented RoSHA [4] an architecture for self-healing robotic systems  implemented in ROS. Their approach relies on monitoring, diagnosis, recovery  management and execution. In order to implement the automatic diagnosis,  RoSHA relies on the standard tool ros/diagnostics to collect runtime failure  information (i.e., w.r.t. component dependencies, communication, and time  relations between components) to identify why the robot fails. The collected  information is regarded as symptoms, which are fed into a Bayesian network  in order to compute the correlations between symptoms and root causes. Both  techniques for diagnosis require structural constraints in the model to be feasible,  asking for manual assistance to the diagnosis.

#### Multi-robot diagnosis

Morais et al. [5], promotes an approach for collaborative  fault diagnosis using behavior trees in an agent programming language style,  namely Rason [5]. The approach relies on deploying an extra robot to assist a  faulty robot in diagnosing a fault. Whenever the faulty robot identifies a verdict  of fault in their behavior, the extra robot is activated to examine and provide  extra information to disambiguate the diagnostic. For example, when a faulty  robot does not identify that there is a mechanical issue with their wheel and  cannot reach their destination (verdict), the extra robot examines their wheel  with a camera and identifies an issue. Following the analogy, the testing team  may consider the deployment of extra robots to collect more information to assist  with the diagnostics. Swarmbug [6] is an approach for debugging configuration  bugs in swarm robotics. It abstracts the impacts of environment configurations.  2  (e.g., obstacles) on the drones in a swarm and automatically generates, validates, and ranks fixes for configuration bugs.

Strengths:

A benefit of postmortem analyses in comparison to on-the-fly analyses is that  the former, with full traces, presents better potential to improve the explanation  precision [1].

Weaknesses:

Diagnosis may require manual effort and domain knowledge to be effective,  diagnosing without domain experience may lead to false positives.

References

> [1] Y. Falcone, S. Krsti´c et al., “A taxonomy for classifying runtime verification  tools,” International Journal on Software Tools for Technology Transfer,  vol. 23, no. 2, pp. 255–284, 202
>
> [2] F. Roman, R. G. Maidana et al., “Overseer: A multi robot monitoring infrastructure,”  in International Conference on Informatics in Control, Automation  and Robotics (ICINCO), 2018, Brasil., 2018.
>
> [3] M. A. Hossen, S. Kharade et al., “Care: Finding root causes of configuration  issues in highly-configurable robots,” IEEE Robotics and Automation Letters,  2023.
>
> [4] D. Kirchner, S. Niemczyk et al., “Rosha: A multi-robot self-healing architecture,”  in Robot Soccer World Cup. Springer, 2013, pp. 304–315.
>
> [5] M. G. Morais, F. R. Meneguzzi et al., “Distributed fault diagnosis for multiple  mobile robots using an agent programming language,” in 2015 International  Conference on Advanced Robotics (ICAR). IEEE, 2015, pp. 395–400.
>
> [6] C. Jung, A. Ahad et al., “Swarmbug: debugging configuration bugs in  swarm robotics,” in Proceedings of the 29th ACM Joint Meeting on European  Software Engineering Conference and Symposium on the Foundations of  Software Engineering, 2021, pp. 868–880.  3
---------------------------------- GUIDELINE CONTENT END ----------------------------------
