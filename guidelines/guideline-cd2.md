---
title: "CD2. Ensure global time monotonicity of events and states"
permalink: /guidelines/guideline-cd2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [timing, synchronization, developer, ros2]
---

## Context (WHEN)

> As distributed systems, such as ROS-based applications, rely on time scheduling for their operation, ensuring time monotonicity is crucial to guarantee the replicability and reproducibility of test cases. Non-determinism in the scheduling of events can lead to unexpected behavior, compromising the reliability of tests and hindering their reproduction. To address this issue, developers must ensure that the testing team is aware of the expected behavior given the occurrence of events, which requires establishing a clear execution order and priority. For instance, by synchronizing different data types at package or subscription level [1].

## Reason (WHY)

Ensuring global time monotonicity of events and states permits addressing the potential non-determinism in the scheduling of events in ROS-based applications.

## Suggestion (WHAT)

The development team should ensure global time monotonicity of events and states to avoid potential non-determinism in scheduling. Such non-determinism is a threat to getting confidence in the system since repeated tests under the same conditions may turn into different results. A technique that can be used to ensure determinism is annotating messages and requests with timestamps and implementing a logical time synchronizer, similar to what is done by MAVROS (git:[mavlink/mavros](https://github.com/mavlink/mavros)). Also, the Time Synchronizer message filter (wiki:[message_filters](http://wiki.ros.org/message_filters)) may be used for this purpose.

## Process (HOW)

Events are said to be monotonic in time whenever for a set of events scheduled over a global clock, two consecutive events are successive. First, the developers should understand how events are scheduled and the limitations of the application towards predictable ordering of events [2, 3]. Then, the developers should analyze and guarantee that all processes are executed in the expected order and will lead to predictable behavior. Developers may accomplish such analysis and guarantee provision with external tools, for instance, formal methods [4, 5] or by embedding timestamps (e.g., SteadyTime) and filtering messages to guarantee ordered events (e.g., MAVROS).

## Exemplars

#### Understand the scheduling of ROS events and states

Chaaban K. [2] explains that ROS 2 schedules callbacks using a non-preemptive algorithm that consumes messages depending on their type. Unlike typical real-time priority based scheduling algorithms, ROS 2 does not execute callbacks in their activation instances. Thus non-time-based messages are scheduled in a round-robin fashion. To this extent, ROS 2 (which claims to address real-time) presents limitations when asked for well-defined execution orders and priority inversion. Choi et al. [3] promotes ros2-picas (git:[rtenlab/ros2-picas](https://github.com/rtenlab/ros2-picas)), a new scheduling algorithm that adds priority awareness for scheduling in ROS2.

#### Analyse starvation-freedom to support monotonicity

Blaß T. et al. [4] propose a response-time analysis exploiting the round-robin properties. The authors present an analysis of starvation-freedom using three techniques: modeling processor demand as execution-time curves instead of scalar worst-case execution times (WCETs), accounting for the effects of quiet times and busy windows in the activation curve derivation, and exploiting the round-robin behavior of the ROS callback scheduler. Starvation freedom indicates monotonicity and ordering of events, it helps the developers to understand real-time behavior and set expectations.

Halder R. et. al [5] use model checking (e.g., UPPAAL [6]) to analyze real-time behavior in ROS-based applications. Under the claim that ROS non-deterministically empties the communication queues, the authors focus on modeling the message-passing behavior of ROS and verifying whether the queue overflows. Since overflow here means that some process is starving, thus the application is not monotonic in time. The authors offer the models in timed automata and TCTL (Temporal Computational Tree Logic) properties designed to ensure real-time for the safety controller of the[Kobuki](http://wiki.ros.org/kobuki)exemplar.

#### Annotating messages with timestamps and synchronization to guarantee ordering

The SteadyTime[(SteadyTime)](https://design.ros2.org/articles/clock_and_time.html)class in ROS represents a monotonic clock, functioning independently of physical time and with steady tick times. MAVROS[(MAVROS)](https://github.com/mavlink/mavros), a library broadly used in ArduPilot for flight control, approaches time monotonicity guarantees by implementing a logical time synchronizer. The synchronizer ensures that the time passing in MAVROS is aligned with the time on ArduPilot’s side, avoiding drifts that could lead the application to fail. More importantly, the time synchronizer uses a particular type of message that embeds timestamps for clock synchronization for updating ArduPilot about its[time status](https://github.com/mavlink/mavros/blob/ros2/mavros_msgs/msg/TimesyncStatus.msg). Messages such as this can be used for synchronizing the occurrence of events in the system. The Time Synchronizer message filter, for example, reads timestamps from the header of messages and synchronize messages by outputting channels to a single callback.

Strengths:

Tests reliability increases by enabling the prediction of the expected behavior of a system under scrutiny. In addition, time monotonicity guarantees can facilitate reproducing test results by establishing a clear execution order and priority. Finally, developers can reduce the time taken and resources used to verify the system behavior by implementing time synchronization and annotation messages with timestamps

Weaknesses:

Implementing time synchronization to ensure time monotonicity may require additional development effort, adding complexity to the system. Also, time synchronization may add performance overhead due to additional operations execution. Achieving real-time behavior depends on the (interaction with the) operating system.

References

> [1] I. Malavolta, G. A. Lewis et al., “Mining guidelines for architecting robotics software,” Journal of Systems and Software, vol. 178, p. 110969, 2021.
>
> [2] K. Chaaban, “A new algorithm for real-time scheduling and resource mapping for robot operating systems (ros),” Applied Sciences, vol. 13, no. 3, p. 1532, 2023.
>
> [3] H. Choi, Y. Xiang et al., “Picas: New design of priority-driven chain-aware scheduling for ros2,” in 2021 IEEE 27th Real-Time and Embedded Technology and Applications Symposium (RTAS). IEEE, 2021, pp. 251–263.
>
> [4] T. Blaß, D. Casini et al., “A ros 2 response-time analysis exploiting starvation freedom and execution-time variance,” in 2021 IEEE Real-Time Systems Symposium (RTSS). IEEE, 2021, pp. 41–53.
>
> [5] R. Halder, J. Proenca et al., “Formal verification of ros-based robotic applications using timed-automata,” in 2017 IEEE/ACM 5th International FME Workshop on Formal Methods in Software Engineering (FormaliSE). IEEE, 2017, pp. 44–50.
>
> [6] J. Bengtsson, K. Larsen et al., “Uppaal—a tool suite for automatic verification of real-time systems,” in Proceedings of the DIMACS/SYCON Workshop on Hybrid Systems III: Verification and Control: Verification and Control. Berlin, Heidelberg: Springer-Verlag, 1996, p. 232–243.
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
