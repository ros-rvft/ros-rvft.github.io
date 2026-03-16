---
title: "I2. Provide an API for logging and filtering"
permalink: /guidelines/guideline-i2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [logging, instrumentation, developer]
---

## Context (WHEN)

> Dynamically gathering information is a fundamental step for gaining confidence in ROS-based systems. Logging (and playback) is, in fact, one of the most used techniques for testing ROS-based systems [1]. Often named monitoring [2], or logging [3], the process of recording textual or numerical information about events of interest may be a valuable input to the testing team. With such data in hand, the testing team will process the data and transform it into useful information to challenge their hypotheses about how the system should work.

## Reason (WHY)

Logging important events
          depends on instrumenting the code (with ‘hooks’) that
          enables the information retrieval activity. It is unrealistic
          to assume that the testing team will have access to the source
          code or that the testing team knows what events to log or
          how to do so.

## Suggestion (WHAT)

The development team should provide an API for logging and filtering data to enable access to valuable runtime data which should be used for both runtime verification and field-based testing. The standard approach to logging and filtering is rosbag (wiki:[rosbag](http://wiki.ros.org/rosbag)). Though, in addition, AWS CloudWatch (git:[aws-robotics/cloudwatchlogs-ros2](https://github.com/aws-robotics/cloudwatchlogs-ros2)) collects data from the rosout topic and provides a filter for eliminating noise from the logged events. Another example is the Robotic Black Box (git:[ropod-project/black-box](https://github.com/ropod-project/black-box)) which allows for listening to data traffic from distinct sources and logging the messages using MongoDB.

## Process (HOW)

We divide, according to Falcone et al. [2], techniques for gathering information in two: inline, and outline. Inline logging and filtering stand for techniques that ask for actually inserting snippets of code in the system under scrutiny as a means to provide an API for logging, e.g., [4]. Outline logging and filtering stands for techniques that enable an external means to gather and filter information that does not require changing the source code, e.g., [5, 6, 7]. Developers may choose one or another given their domain of application.

## Exemplars

#### Inline logging and filtering

ROS, by standard, contains a system-wide string logging mechanism, namely[ROS logging](http://wiki.ros/logging). ROS logging works with a set of macros defined for instrumenting the nodes with information hooks. In the background, the macros send messages with the information to be logged through a standard topic called rosout. On the other side of the topic, an extra node, within the roscore package, persists the data in a textual format[rosout](https://github.com/ros/ros_comm/blob/noetic-devel/clients/rospy/src/rospy/impl/rosout.py). Developers can use the macros to log information that might be used for testing in a later stage, given the application-specific requirements. 
          For instance, the Amazon AWS service for robotics provides AWS CloudWatch Logs[(aws-robotics/cloudwatchlogs-ros2)](https://github.com/aws-robotics/cloudwatchlogs-ros2)interfaces directly with rosout to monitor applications using the standard ROS logging interface. In addition, the standard library provides logging macros with embedded filtering capabilities, which enables eliminating noise from the logged events and can render a useful tool for testers. ROS Rescue is another example of inline logging for ROS 1. The tool aims at solving the problem of ROSMaster as a single point of failure. The authors approach check-pointing and restoring state by logging changes in the metadata stored in the master node. Such metadata contains URIs from various nodes, port numbers, published or subscribed topics, services, and parameters from the parameter server. Kaveti P. et al. create an API for the[ROS master node](https://github.com/PushyamiKaveti/fault-tolerant-ros-master/blob/master/src/ros_comm/rosmaster/src/rosmaster/master_api.py)using the official logging library from Python to persist metadata in YAML format. Their technique opens space for further inspection of ROS applications without access to the source code

#### Outline logging and filtering

[ROSMonitoring](https://github.com/autonomy-and-verification-uol/ROSMonitoring/blob/master/generator/online_config.yaml)[5] employs monitors to persist events in textual format. The monitors contain filtering capabilities to eliminate entries that are inconsistent with the specification (requires an oracle). In this context, the launch files to configure ROSMonitoring can be seen as an API for logging and filtering. Monitors in ROSMonitoring are nodes, thus, the API is a set of known topics and message formats. The tester, in that case, only needs to specify what topics ROSMonitoring will listen to and the type of message to be recorded. The logging and filtering happen within a separate service.

On a similar stance, and inspired by aircraft black box (and software black box [6]), Mitrevski, et al. [7] propose the concept of[Robotic Black Box](https://github.com/ropod-project/black-box). The black box operates as an isolated component responsible for listening to data traffic from distinct sources and logging in an easily retrievable medium. Similarly to ROSMonitoring, Mitrevski’s black box approach to logging inspects topics and message types that are configured in advance. Different from ROSMonitoring, Robotic Black Box offers logging not only in textual format but also in a MongoDB database, which is essentially useful for data processing, filtering, and retrieval. Robotic Black Box stands out when it comes to its filtering and retrieval capabilities. The approach builds a customized query interface over the MongoDB database using names of collections, timestamps and metadata to filter the results.

Strengths:

An API for retrieval and filtering facilitates access to valuable information resulting in effortless observability of inner states and events

Weaknesses:

Overuse of logging may result in performance issues. Incorrectly implemented logging and filtering capabilities may lead to noise in the data, impacting the reliability of the tests. Finally, insufficient logging may result in an incomplete assessment of the system behavior and might generate false positives.
---------------------------------- GUIDELINE CONTENT END ----------------------------------
References

> [1] A. Afzal, C. Le Goues et al., “A study on challenges of testing robotic systems,” in 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020, pp. 96–107.
>
> [2] Y. Falcone, S. Krsti´c et al., “A taxonomy for classifying runtime verification tools,” International Journal on Software Tools for Technology Transfer, vol. 23, no. 2, pp. 255–284, 2021.
>
> [3] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [4] P. Kaveti and H. Singh, “Ros rescue: fault tolerance system for robot operating system,” Robot Operating System (ROS) The Complete Reference (Volume 5), pp. 381–397, 2021.
>
> [5] A. Ferrando, R. C. Cardoso et al., “Rosmonitoring: a runtime verification framework for ros,” in Annual Conference Towards Autonomous Robotic Systems. Springer, 2020, pp. 387–399.
>
> [6] S. Elbaum and J. C. Munson, “Software black box: an alternative mechanism for failure analysis,” in Proceedings 11th International Symposium on Software Reliability Engineering. ISSRE 2000. IEEE, 2000, pp. 365–376.
>
> [7] A. Mitrevski, S. Thoduka et al., “Deploying robots in everyday environments: Towards dependable and practical robotic systems,” arXiv preprint arXiv:2206.12719, 2022.
>
> >
