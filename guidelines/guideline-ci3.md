---
title: "CI3. Identify safety constraints"
permalink: /guidelines/guideline-ci3
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [safety, constraints, runtime-verification, developer]
---

## Context (WHEN)

> The assessment of safety constraints is essential for both runtime verification and field-based testing. When stimulating robotic systems with extreme scenarios, for instance in robustness testing [1], it’s crucial to consider potential threats to personnel and the properties being tested. These threats limit the ability to conduct online assessments for safety-critical applications, particularly in robotics. To ensure the benefits of field-based testing [2], it’s important to carefully address and compensate for the introduced safety risks. Non-negotiable safety constraints should be maintained throughout the confidence-gathering process, as they determine the readiness and release of technology, both in industry and everyday use [3].

## Reason (WHY)

Safety hazards may unable runtime verification or field-based testing since corner cases may pose threats to testing personnel or damage property during runtime assessment.

## Suggestion (WHAT)

The developers should identify the boundaries of a safe behavior (i.e., safety constraints) to enable the use of mechanisms for preventing the robot from hurting operators or property during testing and verification activities. For example, the developers can identify constraints like speed limit, distance to obstacle, or conditions for emergency stop, which can be used by monitoring tools like ROSMonitoring (git:[autonomy-and-verification-uol/ROSMonitoring](https://github.com/autonomy-and-verification-uol/ROSMonitoring)), or used by an independent safety controller in a separate ROS node to prevent the robot from falling from a cliff, e.g., the Kobuki robot (git:[yujinrobot/kobuki](https://github.com/yujinrobot/kobuki)).

## Process (HOW)

Safety constraints may be specified in using many specification languages. The known toy example in mobile robotics, Kobuki, specifies safety properties in a separate ROS node using the switch-case in Python; Adam et al.[4] proposes rule-based specifications in the format of boolean equations that predicate over messages over topics; Stadler et al. [5], uses an event processing language offering query-based operations; Finally, Huang et. al [6] enables the specification of temporal properties leveraging monitoring-oriented programming (MOP).

## Exemplars

#### Typical safety constraints

- Emergency stop, [4]
- Speed monitoring (e.g., $v < 0.2m/s$) [4]
- Movement speed limit (e.g., speed limit $0.35 m/s) [5]
- Timing monitoring (e.g., $t > 10$) [4]
- Obstacle avoidance (e.g., maintain at least $35cm$ distance from object) [5]
- Joint effort (e.g., max joint effort) [5]

The Kobuki robot implements a[safety controller](https://github.com/yujinrobot/kobuki/blob/23748ed3dfb082831ca8eaaef1a0b08588dbcb65/kobuki_safety_controller/include/kobuki_safety_controller/safety_controller.hpp). The kobuki's safety controller specifies, using Python at code-level, a state machine ensuring that the robot stops whenever it is close to a cliff, the bumper sensor was pressed, or at least one of the wheels dropped (or was raised in the air). The Kobuki's safety controller is a separate ROS node collecting bumper, cliff and wheel events. A sequence of events may trigger an alert or issues velocity commands to deviate Kobuki from the threat.

Adam S. et al. [4] defines a rule-based language for enforcing safety constraints on existing ROS-based software. Their approaches uses a simplified metamodel to describe the ROS software enabling static analysis as well as invariant monitoring. The authors explain that separating the specification of safety issues from functionality facilitates attesting that the robotic behavior conforms to safety requirements. Their rule-based approach enables the specification of actions that preclude rules encoded in boolean equations (e.g. cmd vel left > 0.02m/s) over messages in topics.

Stadler et al., [5] uses the Esper Constraint Engine to check for violations of the safety constraints. Such constraints are specified using the EPL notation. Event Processing Language (EPL) is a SQL-standard language with extensions, offering SELECT, FROM, WHERE, GROUP BY, HAVING and ORDER BY clauses. For instance, they specify that an event such as JointEffortEvent (AEvent) will not exceed a maximum of 5.0 in an ESL constraint specification (i.e.[max joint effort constraint](https://github.com/MStadler-Organization/ROMoSu/blob/main/services/constraint_engines/src/main/resources/constraints/c1_mx_joint_effort.cst)).

Listing 1: Safety constraint in EPL notation.

```
select * from AEvent(MaxValue > 5.0)
```

Huang et al.'s [6] monitoring infrastructure enables the use of any logic plugins of Monitoring-Oriented Programming, thus enabling specification of temporal properties over events, such as regular expressions, linear temporal logics, and context-free grammars. For instance, one of their monitors predicates on the position of the turret installed in the autonomous vehicle, i.e., ``the gun should not exceed a maximum joint angular position otherwise the turret targets itself.''.

Strengths:

By identifying safety constraints, developers can demonstrate compliance with these requirements, providing assurance to stakeholders that appropriate safety measures are in place. Early detection and response to safety violations, such as exceeding speed limits or approaching obstacles too closely. This early detection and response can help prevent accidents and minimize potential damage.

Weaknesses:

Identification of safety hazards involves understanding the system's behavior, identifying potential risks, and formulating appropriate constraints. This process can be time-consuming and complex, especially for large and intricate systems, potentially increasing development costs.

References

> [1] A. Afzal, C. Le Goues et al., “A study on challenges of testing robotic systems,” in 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020, pp. 96–107.
>
> [2] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [3] D. Bozhinoski, D. Di Ruscio et al., “Safety for mobile robotic systems: A systematic mapping study from a software engineering perspective,” Journal of Systems and Software, vol. 151, pp. 150–179, 2019.
>
> [4] S. Adam, M. Larsen et al., “Towards rule-based dynamic safety monitoring for mobile robots,” in Simulation, Modeling, and Programming for Autonomous Robots: 4th International Conference, SIMPAR 2014, Bergamo, Italy, October 20-23, 2014. Proceedings 4. Springer, 2014, pp. 207–218.
>
> [5] M. Stadler and M. Vierhauser, “Romosu: Flexible runtime monitoring support for ros-based applications,” in RoSE’23: 5th International Workshop on Robotics Software Engineering Proceedings, 2023, p. xx.
>
> [6] J. Huang, C. Erdogan et al., “Rosrv: Runtime verification for robots,” in International Conference on Runtime Verification. Springer, 2014, pp. 247–254.
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
