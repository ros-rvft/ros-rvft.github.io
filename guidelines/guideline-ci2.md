---
title: "CI2. Identify security and privacy constraints"
permalink: /guidelines/guideline-ci2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> Runtime assessment introduces challenges to security and privacy preservation. Modifying the source code to facilitate testing may, however, open space for security and privacy exploitation[1]. From the point-of-view of runtime verification, security and privacy preservation revolves around specifying flavors of integrity, confidentiality, and availability[2]. For instance, Autonomous Driving Vehicles (ADVs) regulators define policies given the territory they are being used in. However, ADS introduction also requires public trust, w.r.t security and safety [3]. In a scenario of runtime assessment, be it field-based testing or runtime verification, security and privacy exploits may be catastrophic. Yet, security is still under-explored when it comes to architectural designs for ROS-based applications [4].

## Reason (WHY)

Security and Privacy are often under-explored in the design of ROS-based applications. Threats to privacy and security may be catastrophic and may be an unacceptable side-effect of runtime assessment of such robotic applications.

## Suggestion (WHAT)

The development team should identify security or privacy vulnerabilities that may pose a risk to participants' integrity, confidentiality, and availability, that may be caused by the testing and runtime verification activities. The ros-security workgroup maintains SROS (git:[ros2/sros2](https://github.com/ros2/sros2)) for the analysis of such vulnerabilities and fixes. In addition, Alias Robotics maintains a database of vulnerabilities detected in ROS applications (git:[aliasrobotics/RVD](https://github.com/aliasrobotics/RVD)) as a means of awareness.

## Process (HOW)

Jeong S. Y. et al. [5] list a set of vulnerabilities typically encountered in ROS applications, including broken authentication, the rosbag replay attack, and service hijacking. Neither preparing the code for runtime assessment nor the runtime assessment procedure itself should enable or facilitate the exploitation of such vulnerabilities. The developers must be aware of such vulnerabilities and specify constraints specific to the domain of the application, enforcing or informing the testing of the danger. From one side, the ros-security working group works on mitigating security vulnerabilities provided by design from ROS [6]. From another stance, other approaches focus on confidentiality, integrity, and availability while providing means to specify control access policies and generate firewall rules based on the fundamental elements of ROS [7, 8].

## Exemplars

#### FAST-DDS

[FAST-DDS](https://fast-dds.docs.eprosima.com/en/latest/fastdds/security/security.html)is the current technology used in ROS 2. FAST-DDS enables features such as authentication of domain participants using a Certificate Authority (CA), access control to constrain specific operations, authenticated encryption following the Authentication Encryption Standard (AES), logging security events, and data tagging by enabling security labels to data. In addition, the ros-security working group, in tandem with Alias Robotics, works on SROS, a tool for securing ROS within the DevOps model ([ros2/sros2](https://github.com/ros2/sros2)) [6].

Hu et al. specify security properties of ROS-based systems [7]. The specified security properties follow the definition of a composite of attributes on confidentiality, integrity, and availability, according to Avizienis [9]. Hu et al. define the properties following two scenarios: (i) attackers get access to a ROS node and freely allocate memory until reaching an out-of-memory state, (ii) topics or services are hijacked, and the information flowing between ROS nodes is changed to provoke a failure. In such scenarios, the developer’s team should specify constraints to the runtime assessment procedure placing a barrier to facilitating the control of ROS nodes in such a way that enables free memory allocation and should specify conditions to allow ROS topics and services remapping without any certification, for instance. The testing team may want to assess whether their runtime assessment will open up exploit opportunities given a set of constraints.

#### ROSRV

[ROSRV](https://github.com/cansuerdogan/ROSRV/blob/master/docs/Usage.md), a runtime verification framework for safety and security properties of ROS-based applications, provides a specification language for access control policies and enforces them at runtime [8]. Such access control policies may prevent the system from exploiting security breaches, such as enabling the control of safety-critical nodes to the application. More specifically, ROSRV provides access control specifications based on a user-provided specification of access policies using text file inputs. The policies are defined under five categories: groups, nodes, publishers, subscribers, and commands. Nodes represent node names and machine identities, publishers/subscribers define topic names and node identity associated, and commands define the access policy, e.g., full access, localhost (ROSRV).

Strengths:

Identifying security and privacy constraints can help protect participants and resources during runtime assessment. This guideline encourages developers to consider security and privacy early on in the design process, rather than as an afterthought. It encourages the development of more secure and trustworthy ROS-based applications and runtime assessment of ROS-based applications, which can improve public trust and acceptance.

Weaknesses:

The guideline, intentionally, does not provide specific details on how to implement security and privacy constraints, leaving it up to the developers to decide which constraints are necessary and how to enforce them, since this is domain-dependent. It may be challenging to understand the various security vulnerabilities associated with ROS-based applications, making it difficult to specify appropriate security and privacy constraints. The guideline may require additional time and resources to implement security and privacy constraints, which may delay the development process. Systems with lower technology readiness levels, such as academic prototypes, may not need a thorough security assessment, making this guideline irrelevant in those cases.

References

> [1] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [2] Y. Falcone, S. Krsti´c et al., “A taxonomy for classifying runtime verification tools,” International Journal on Software Tools for Technology Transfer, vol. 23, no. 2, pp. 255–284, 2021.
>
> [3] M. Luckcuck, M. Farrell et al., “Formal specification and verification of autonomous robotic systems: A survey,” ACM Computing Surveys (CSUR), vol. 52, no. 5, pp. 1–41, 2019.
>
> [4] I. Malavolta, G. A. Lewis et al., “Mining guidelines for architecting robotics software,” Journal of Systems and Software, vol. 178, p. 110969, 2021.
>
> [5] S.-Y. Jeong, I.-J. Choi et al., “A study on ros vulnerabilities and countermeasure,” in Proceedings of the Companion of the 2017 ACM/IEEE International Conference on Human-Robot Interaction, 2017, pp. 147–148.
>
> [6] V. Mayoral-Vilches, R. White et al., “Sros2: Usable cyber security tools for ros 2,” in 2022 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE, 2022, pp. 11 253–11 259.
>
> [7] C. Hu, W. Dong et al., “Runtime verification on hierarchical properties of ros-based robot swarms,” IEEE Transactions on Reliability, vol. 69, no. 2, pp. 674–689, 2019.
>
> [8] J. Huang, C. Erdogan et al., “Rosrv: Runtime verification for robots,” in International Conference on Runtime Verification. Springer, 2014, pp. 247–254.
>
> [9] A. Avizienis, J.-C. Laprie et al., “Basic concepts and taxonomy of dependable and secure computing,” IEEE transactions on dependable and secure computing, vol. 1, no. 1, pp. 11–33, 2004.
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
