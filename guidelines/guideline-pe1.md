---
title: "PE1. Understand the overhead acceptance criteria"
permalink: /guidelines/guideline-pe1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> According to practitioners, performance is among the three most important quality attributes when designing a robotic application in ROS [1]. Performance is often important in robotics because many computations performed by robots tend to be data-intensive, e.g., computer vision, planning, and navigation [1]. Gaining confidence in robotic applications, then, should not interfere with the nominal performance of the robot under scrutiny. Less (or no) impact on performance is especially desirable when the assurance gathering process interacts with the running system, for instance, in-the-field testing and runtime verification. We name the extra load available for gaining confidence on ROSbased applications as overhead acceptance criteria. The overhead acceptance criteria can be allocated to monitoring, isolation, or maintaining the security of privacy during the runtime assessment session [2].

## Reason (WHY)

A rule of thumb says that more observations tend to enable more precise assurance arguments within a limit. Observing, however, is never free from side effects, incurring in overhead [3]. Therefore, the quality assurance team must contrast the precision of the assurance arguments against overhead introduced by the observation medium. The overhead acceptance criteria are the basis for deciding the runtime assurance strategy.

## Suggestion (WHAT)

The use of runtime verification or field-based techniques might add computation overhead. The QA team should understand how much overhead is acceptable; this is important to decide on a test strategy that will not severely impact the performance of the running system. Such overhead may be due to monitoring with ros tracing (git:[ros2/ros2_tracing](https://github.com/ros2/ros2_tracing)), component isolation, or security and privacy maintenance overhead with ROSploit (git:[seanrivera/rosploit](https://github.com/seanrivera/rosploit)).

## Process (HOW)

Typically, understanding the overhead acceptance criteria follows from contrasting the required performance for delivering the required service, aka nominal performance (e.g., time to reaction, latency, speed), against available resources (e.g., computing power). The QA team may use off-the-shelf ROS tooling, like[ApexAI/Performance](https://gitlab.com/ApexAI/performance_test)test ß, to understand the nominal performance of the ROS-based application. The difference between nominal performance and expected performance may be allocated to the overhead acceptance criteria. If the nominal performance is close enough to the expected performance, there 1 is not enough space for implementing runtime assurance techniques. We categorize three types of overhead that may affect the runtime assurance process: Runtime Monitoring [4, 5], Isolation overhead [6, 7], and Security and Privacy overhead [8, 9].

## Exemplars

#### Monitoring overhead

Monitoring overhead is all extra load put on the system-under-test due to gathering, interpreting, and elaborating data about the execution. For example,[ROSMonitoring](https://github.com/autonomy-and-verification-uol/ROSMonitoring)[4] determines the monitoring overhead by calculating the delay introduced in the message delivery time between ROS nodes. The authors analyse the overhead by varying the size of the system under monitoring, message passing frequency, and number of monitor nodes. However, their overhead analysis is not transparent with respect to gathering, interpreting or elaborating on data, the analysis looks at the monitoring overhead as a black box.

Another example is[ros2/ros2_tracing](https://github.com/ros2/ros2_tracing)[5] that provides a tool or tracing ROS2 systems with low latency overhead. The authors measure monitoring overhead by collecting the time between publishing a message and when it is handled by the subscription callback. In short, monitoring and tracing tools add some overhead that typically affects the message passing latency, the QA team must understand and define a precise time allowance to this overhead.

#### Isolation overhead

Isolation overhead is all extra load put on the system-under-test for guaranteeing that the runtime assessment will not interfere with the normal operation or produce undesired side effects. As an example, Lahami M. et al. [6] propose a safe and resource-aware approach to test dynamic and distributed systems. Safe by employing testing isolation techniques such as BIT-based, tagging-based, aspect-based, cloning-based, and blocking-based. Resource aware by setting resource monitors such as processor load, main memory, and network bandwidth. The authors show that the overall overhead is relatively low and tolerable, mainly if dynamic adaptations are not commonly requested. However, there is no fine-grained evaluation of the overhead introduced by isolation techniques. In fact, isolation overhead is rarely reported [7].

#### Security and Privacy overhead

Security and Privacy overhead is all extra load put on the system-under-test for maintaining security and privacy constraints while testing. For example, ROS-Immunity is a security tool for preventing ROS-based applications from malicious attackers. Rivera S. et al. [8], determine the overhead for maintaining the ROS-based system secure, while operating, in terms of power consumption (in Watts) by comparing the power draw of the system with and without their tool. From another stance, Breiling B. et al [9] present a secure communication channel to enable communication between ROS nodes using protocols such as Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS) per each ROS topic in the application. The protocols follow three steps: an initial handshake with mutual authentication, using symmetric encryption (AES-256), and using Message Authentication Codes (MAC) for data integrity. Importantly, 2 they evaluate the overhead introduced for each step, totaling in a few percentage points (2%-5%) of increase in average CPU load.

Strengths:

Understanding the overhead acceptance criteria in advance may avoid unexpected interruptions in the ROS application functionality due to runtime quality assessment procedures. For example, when testing procedures are mistakenly scheduled whenever the ROS-based application is operating under a high load. Learning about the overhead in advance criteria may also ask for re-design due to a lack of verifiability during runtime. For example, when the nominal performance of the ROS system is close to the expected performance, in value.

Weaknesses:

Although there is tooling to support the assessment of the overhead acceptance criteria, the process for understanding involves executing the system, collecting performance data and analysis. This may conflict with time-to-market requirements, asking for further
negotiation with the business goals of the ROS-based system.

References

> [1] I. Malavolta, G. A. Lewis et al., “Mining guidelines for architecting robotics software,” Journal of Systems and Software, vol. 178, p. 110969, 2021.
>
> [2] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [3] Y. Falcone, S. Krsti´c et al., “A taxonomy for classifying runtime verification tools,” International Journal on Software Tools for Technology Transfer, vol. 23, no. 2, pp. 255–284, 2021.
>
> [4] A. Ferrando, R. C. Cardoso et al., “Rosmonitoring: a runtime verification framework for ros,” in Annual Conference Towards Autonomous Robotic Systems. Springer, 2020, pp. 387–399.
>
> [5] C. Bedard, P.-Y. Lajoie et al., “Message flow analysis with complex causal links for distributed ros 2 systems,” Robotics and Autonomous Systems, vol. 161, p. 104361, 2023.
>
> [6] M. Lahami, M. Krichen et al., “Safe and efficient runtime testing framework applied in dynamic and distributed systems,” Science of Computer Programming, vol. 122, pp. 1–28, 2016.
>
> [7] S. Silva, A. Bertolino et al., “Self-adaptive testing in the field: are we there yet?” in Proceedings of the 17th Symposium on Software Engineering for Adaptive and Self-Managing Systems, 2022, pp. 58–69.
>
> [8] S. Rivera and R. State, “Securing robots: An integrated approach for security challenges and monitoring for the robotic operating system (ros),” in 2021 IFIP/IEEE International Symposium on Integrated Network Management (IM). IEEE, 2021, pp. 754–759.
>
> [9] B. Breiling, B. Dieber et al., “Secure communication for the robot operating system,” in 2017 annual IEEE international systems conference (SysCon). IEEE, 2017, pp. 1–6.
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
