---
title: "CI1. Identify timing constraints"
permalink: /guidelines/guideline-ci1
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> Timing constraints, also known as “deadline” or “timing requirements”, define temporal requirements that real-time systems must adhere to [1]. These constraints can be categorized as soft, firm, or hard, and they play a significant role in determining whether the system respects timing concerns. Since ROS-based systems often involve control nodes (such as attitude control and state estimation [2]), which typically have real-time requirements, identifying timing constraints becomes even more critical.

## Reason (WHY)

Identifying timing constraints is crucial for ROS-based systems as these constraints define the system’s temporal requirements. However, a recent study highlights the lack of support for real-time constraints in the software engineering research of ROS-based robotic systems, emphasizing the need for more attention in this domain [3]. Initially conceived as a means to handle difficult or costly to reproduce failures, field testing has seen limited studies addressing real-time issues, particularly in the realm of autonomous systems [4].

## Suggestion (WHAT)

The development team should identify timing constraints to ensure that no real-time requirements will be neglected during the system testing. For instance, Autoware Perf (git:[azu-lab/ROS2-E2E-Evaluation](https://github.com/azu-lab/ROS2-E2E-Evaluation)) allows for the calculation of response time and latency in ROS 2 applications; such measurements may be used as hard constraints to testing the system. Also, one may identify realtime constraints with respect to synchronization between robots, sensor data processing time, or fault detection and recovery.

## Process (HOW)

Typical timing constraints that cross-cut in robotics domains stand for response time [5], latency, synchronization time [6], fault detection and recovery time, and power management time. The means to specify such constraints vary from informal to formal languages (we invite the interested reader to check guidelines of the group property specification - SDB1 and SDB2. The developers team may use Autoware Perf [7] to calculate response time and latency, for example.

## Exemplars

#### Typical Timing Constraints

Real-time constraints may be subject to the domain and the objectives of the runtime assessment. We provide a comprehensive list of constraints that may be interesting to address when considering testing ROS-based systems. We use Autoware_Perf[(Autoware_Perf)](https://github.com/azu-lab/ROS2-E2E-Evaluation)[7]  to illustrate how to collect response time and latency with practical examples.

*Response time*is the period a ROS-based system takes to react to one or more stimuli from the environment. Specific to the ROS domain, Chaaban, K. defines response time in ROS 2 as the*``duration from the release instant to the completion of the job execution''*[5]. To collect callback response time,[Autoware Perf](https://github.com/azu-lab/ROS2-E2E-Evaluation/blob/main/autoware_perf_galactic/tracetools_analysis-galactic_add_tp/tracetools_analysis/analysis/callback_duration.ipynb)defines a function to get durations of callback instances for a given callback objects.

*Latency*is the time a ROS-based system takes to react to a stimulus from the test orchestrating apparatus. Often, field tests include a centralized computer orchestrating the test cases execution and information collection, latency in such cases tends to be significant.[Autoware Perf](https://github.com/azu-lab/ROS2-E2E-Evaluation/blob/main/autoware_perf_galactic/tracetools_analysis-galactic_add_tp/tracetools_analysis/analysis/galactic/e2elatency.ipynb)illustrates how latency can be computed with an example of a ROS 2 service, where they send a goal to the robot and calculate the time for a response

*Synchronization time*is the time taken for a ROS-based system involving more than one robot to share information.

*Sensor Data Processing time*is the time taken to transform raw sensorial input into information ready to be used by reasoners or planners. Lewis et al. conclude that it is difficult to predict how long robots might have to wait between measurements since quantifying data collection for real-time systems needs to account for all the [metereological] sensors and their respective response times [6]

*Fault Detection and Recovery time*is the time taken to prevent safety hazards. Robots, mainly operating in safety-critical scenarios, often have safety mechanisms to prevent hazards. Testing in the field, in general, asks for safety assessment, thus incurring timing overhead.

*Power Management time*is the time taken to prevent stop or graceful degradation due to a power outage. Robots may rely on batteries or other embedded power sources (such as solar panels). Power management may affect the testing conditions and be considered when testing in the field. For example, to start a recharging process in the middle of the mission or to slow the velocity to recharge the batteries using solar energy.

Strengths:

Identifying timing constraints is a good practice to avoid neglecting important real-time requirements during development. It also helps isolate the tested behavior without unintended outcomes due to real-time faults.

Weaknesses:

Specifying timing constraints may be complex due to the ROS nature presenting interconnected components and dependencies. There is a lack of standardization or best practices for specifying such properties. This may result in an overhead when the application is not real-time critical. Property specification guidelines (SDB1, SDB2) will further investigate this issue.

References

> [1] W. Sch¨utz, The testability of distributed real-time systems. Springer Science & Business Media, 2007, vol. 245.
>
> [2] M. Beul, N. Krombach et al., “Autonomous navigation in a warehouse with a cognitive micro aerial vehicle,” in Robot Operating System (ROS). Springer, 2017, pp. 487–524.
>
> [3] M. Albonico, M. Djevic et al., “Software engineering research on the robot operating system: A systematic mapping study,” Journal of Systems and Software, vol. 197, p. 111574, 2023.
>
> [4] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [5] K. Chaaban, “A new algorithm for real-time scheduling and resource mapping for robot operating systems (ros),” Applied Sciences, vol. 13, no. 3, p. 1532, 2023.
>
> [6] T. Lewis and K. Bhaganagar, “Configurable simulation strategies for testing pollutant plume source localization algorithms using autonomous multisensor mobile robots,” International Journal of Advanced Robotic Systems, vol. 19, no. 2, 2022.
>
> [7] Z. Li, A. Hasegawa et al., “Autoware perf: A tracing and performance analysis framework for ros 2 applications,” Journal of Systems Architecture, vol. 123, 2022. 3 -
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
