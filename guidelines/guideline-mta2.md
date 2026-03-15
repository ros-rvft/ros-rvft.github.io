---
title: "MTA2. Exploit automation for test case generation, test case prioritization and selection, oracle and monitor generation"
permalink: /guidelines/guideline-mta2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> Automation of testing activities is getting increasing attention in the robotic domain, even in the case of field-based testing. Automation can be exploited for various activities, including test case generation [1], prioritization, selection, and oracle generation. The benefits brought by automation are various: it helps improving the efficiency, effectiveness, and reliability of the software testing processes, e.g. by increasing the test coverage and providing consistency and repeatability in the testing process. However, when applying automation in testing there are several challenges to be considered [2]. First, it needs to deal with the environmental complexity and its high variability. Second, specifying and/or generating an oracle that automatically distinguishes between correct and incorrect behaviours is not always obvious. Consequently, the test automation in field-based testing, is still limited and relies heavily on human contributions [3].

## Reason (WHY)

Automating testing activities can improve efficiency, as they can be run quickly and repeatedly without human intervention. This leads to quicker feedback on the quality of the software. Also, automation is essential to enhance the efficiency, effectiveness and reliability of the software testing processes. Moreover, as the system grows and evolves, automated test suites can generally be extended easily to accommodate new features and changes. Indeed, there is an initial investment to be made in creating and maintaining the automation machinery.

## Suggestion (WHAT)

The QA team should exploit automation tools for test case generation, test case selection and oracle generation, as well as other testing activities, to efficiently gain confidence in ROS-based systems in the field. For example, Mithra (pdf:[Mithra](https://afsafzal.github.io/materials/AfzalMithra.pdf)) learns oracles from logs generated during the execution, it is motivated by a case from ArduPilot and tested in autonomous racing cars built on ROS. In addition, HAROS (git:[git-afsantos/haros](https://github.com/git-afsantos/haros)) promotes test case generation from properties using a tool called Hypothesis (git:[HypothesisWorks/hypothesis](https://github.com/HypothesisWorks/hypothesis)). Finally, a technical report (pdf:[bergert:2022-iros-roboticstesting](https://www.cse.chalmers.se/$\sim$bergert/paper/2022-iros-roboticstesting.pdf)) details how a company building mobile robots for disinfection uses equivalence partitioning for test case selection for the field.

## Process (HOW)

To effectively implement test automation, one important step concerns the oracle specification, which is a mechanism or criteria to determine whether a test has passed or failed [4]. A novel approach in automatic oracle generation based on telemetry data which is validated using a ROS-based system is proposed in [5]. An important automation activity is the test case generation, with the aim of crafting tests cases to cover various functionalities, scenarios and edge cases of the system. For achieving this, a viable approach is to use Property Based Testing [6], where test cases are automatically generated to target specific properties of the system. Another important automation activity concerns the test selection, which aims to select, in the search for efficiency, the relevant and representative scenarios to be tested. In this area, equivalence testing is a technique that allows us to reduce the amount of test cases used by dividing the generated cases in equivalence classes, as evidenced in [7], where the authors study ROS-based systems in the domain of service robotics.

## Exemplars

#### Technology enablers

As a technology enabler, rostest[(rostest)](http://wiki.ros.org/rostest)is a ROS framework that allows us to do full integration testing across multiple nodes. In the task of test case generation in particular, one crucial component of the library is unit test. This module makes it possible to perform ROS node integration-level tests as well as code-level unit tests. In the case of ROS 2, the testing mechanism is ingrained in the structure of the packages, which makes the test development considerably easier.

#### Oracle specification

In the area of automated oracle generation, the authors of [5] present Mithra, which is a novel and unsupervised oracle learning technique for Cyber-Physical Systems (CPS). The approach is applied to autonomous racing cars built for ROS. The oracle learning approach builds oracles by clustering telemetry logs represented by a novel formulation of multivariate time series (MTS) that effectively and concisely encodes correct CPS behaviour.

#### Test case generation

Santos et al. [6] rely on property-based testing (PBT) to generate test cases driven by properties specified in the form of assertions. The tool Hypothesis[(hypothesis)](https://github.com/HypothesisWorks/hypothesis)receives a model of ROS configurations and generates customizeable property-based scripts for tests aimed at these configurations. It builds on top of configuration models extracted using HAROS, a static analysis framework for ROS applications. As another example, in the domain of mobile robots, the work in [8] presents an approach to automatically generate test cases in the form of stressful trajectories. In essence, the work integrates kinematic and dynamic physical models of the robot to generate valid trajectories. The test case generator incorporates a parameterizable scoring model to efficiently generate valid yet stressful trajectories for a broad range of ROS-based mobile robots.

#### Test case selection

As a test selection mechanism, one commonly used technique is Equivalent Partitioning. The objective of equivalence partitioning is to minimize test case explosion, i.e. reduce the high number of possible combinations of the properties that will be tested. The idea behind Equivalence Partitioning is to group the test cases into equivalence classes according to how they handle valid or invalid data [7]. The authors report the experience of field testing in the domain of service robotics. In particular, the system under study was the Kelo AD disinfection robot whose software stack is based on ROS. To implement the equivalence testing, the criteria for defining the classes included robot motion, person posture, existence of occlusions and obstacle positions.

Strengths:

Automation in testing activities can be executed repeatedly with low effort and cost. Moreover, it brings benefits in terms of efficiency, effectiveness, and reliability.

Weaknesses:

There is a high initial investment of time and resources. There is also a maintenance overhead related to maintaining the automation machinery when the system evolves. Test generation may not scale for complex scenarios.

> [1]  C. Hutchison, M. Zizyte et al., “Robustness testing of autonomy software,” in 2018 IEEE/ACM 40th International Conference on Software Engineering: Software Engineering in Practice Track (ICSE-SEIP). IEEE, 2018, pp. 276–285.
>
> [2]  A. Afzal, C. Le Goues et al., “A study on challenges of testing robotic systems,” in 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020, pp. 96–107.
>
> [3] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [4]  E. T. Barr, M. Harman et al., “The oracle problem in software testing: A survey,” IEEE transactions on software engineering, vol. 41, no. 5, pp. 507–525, 2014.
>
> [5] A. Afzal, C. Le Goues et al., “Mithra: Anomaly detection as an oracle for cyberphysical systems,” IEEE Transactions on Software Engineering, vol. 48, no. 11, pp. 4535–4552, 2021. 2Added after follow-up questionnaire on April 14th. 3
>
> [6] A. Santos, A. Cunha et al., “Property-based testing for the robot operating system,” in Proceedings of the 9th ACM SIGSOFT International Workshop on Automating TEST Case Design, Selection, and Evaluation, 2018, pp. 56–62.
>
> [7] A. Ortega, N. Hochgeschwender et al., “Testing service robots in the field: An experience report,” in 2022 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE, 2022, pp. 165–172.
>
> [8] C. Hildebrandt, S. Elbaum et al., “Feasible and stressful trajectory generation for mobile robots,” in Proceedings of the 29th ACM SIGSOFT International Symposium on Software Testing and Analysis, 2020, pp. 349–362. 4
---------------------------------- GUIDELINE CONTENT END ----------------------------------
