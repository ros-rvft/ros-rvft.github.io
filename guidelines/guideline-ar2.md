---
title: "AR2. Use reliable tooling in order to manage field data"
permalink: /guidelines/guideline-ar2
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> Maintaining the field resources is a fundamental step for the repeatability and reliability of field tests [1]. The field data is useful for generating field test cases and postmortem analyses. Yet, the data generated before, during and after testing must be kept and managed. Field data management often includes storing new data, annotating data, and generating reports. Such activities may turn intractable as the number of trials grows along with the complexity of the stored data (i.e., in perception systems, or learning-enabled systems). Manually managing such data is error-prone and sometimes unfeasible.

## Reason (WHY)

Field testing is expensive and relying on ad hoc solutions to storing data may result in corrupted or incomplete field data. Unreliable tooling may be a source of flaky tests or skewed conclusions about the system (i.e., false-positive results).

## Suggestion (WHAT)

The QA team should use reliable tools for field data management to avoid problems with corrupted, unreliable, and/or incomplete data. For example, the warehouse_ros package offers both MongoDB (git:[ros-planning/warehouse_ros_mongo](https://github.com/moveit/warehouse_ros_mongo)) and SQLite (git:[ros-planning/warehouse_ros_sqlite](https://github.com/moveit/warehouse_ros_sqlite)) database backend for recording states, scenes, and messages. In addition, the Field Test Tool (git:[fkie/field_test_tool](https://github.com/fkie/field_test_tool)) uses the PostgreSQL database manager extended with PostGIS (web:[PostGIS](https://postgis.net/)) for geolocalization.

## Process (HOW)

Testers may use local workspace standard tooling aided by git-based versioning [2] or structured database [3, 4], and file-server [5], for field data management. On the one hand, using local workspace tooling is intuitive since tutorials in ROS traditionally rely on them, and most developers are used to the workspace management tools. On the other hand, structured approaches using database management tools may render easier querying and means to automatic report generation. When it comes to database integration for persisting long-term data, Malavolta et. al suggest using a dedicated node to interface the application and the database system in order to mitigate performance issues [6].

## Exemplars

#### Local workspace with git support

Ortega A. et al. reports about the 1 maintenance of test documents and artifacts for testing in the field [2]. The documents contain the specification of test procedures, reports, rosbag files, incident reports and cases in which people are detected. Test reporting is done on an in-house tool called Technology Readiness Level Test Report Library (TRL) and the reports are stored in a git repository where test incidents issues. TRL is based on the standard tooling for local workspace management in ROS, namely wstool[(wstool)](http://wiki.ros.org/wstool).

#### Database and File-server

The warehouse ros package provides MongoDB[(warehouse_ros_mongo)](https://github.com/ros-planning/warehouse_ros_mongo)and SQLite[(warehouse_ros_SQLite)](https://github.com/ros-planning/warehouse_ros_sqlite)database backend for persistently recording states, scenes and messages, working in conjunction with RViz and the MotionPlanning plugin. The Field Test Tool[(FTT)](https://github.com/fkie/field_test_tool)provides support for logging, annotating, and automatically generating reports of field trials for autonomous ground vehicles [4]. The tool relies on a database to store field data, which is later accessed for automatic report generation. The authors use PostgreSQL database manager extended with PostGIS for geolocalization. The data is stored in the database through an interface ROS node which collects field data (Operation mode, GNSS positioning, local positioning, a map of the environment, and possibly images from a camera) from selected topics. Data collection is started and stopped in a web server that interfaces with the tester. The web interface can also be used to add annotations to collected field data. In addition to FTT, the Overseer architecture [3] enables the persistence of field data in a MySQL database, which can be further accessed by the monitoring system Nagios. On another stance, Hartsell et al. [5] studies ROS-based systems with learned-enabled components. Often, testing such systems is prone to large dataset maintenance, which can be a problem in the field. The author’s approach uses a mix of file servers for storing the data and a database for storing metadata. The file server relies on SSH File Transfer Protocol (SFTP) to store all generated data, resulting from the execution of a job (aka trial), results and notes from the experiments. The metadata is persisted in a version-controlled database for quick retrieval. As far as we are concerned, even though Hartsell’s approach should work for field testing it was only validated in simulation testing [5].

Strengths:

Tool support for persisting field data helps with data reliability since it is less likely that data will be lost or will be corrupted. In addition, this guideline enables traceability of trial execution with possible failure or fault.

Weaknesses:

Using database systems to log long-term data may pose a threat to the performance of the testing apparatus.

References

> [1]  A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [2] A. Ortega, N. Hochgeschwender et al., “Testing service robots in the field: An experience report,” in 2022 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE, 2022, pp. 165–172.
>
> [3] F. Roman, R. G. Maidana et al., “Overseer: A multi robot monitoring infrastructure,” in International Conference on Informatics in Control, Automation and Robotics (ICINCO), 2018, Brasil., 2018.
>
> [4] C. Tampier, A. Tiderko et al., “Field test tool: automatic reporting and reliability evaluation for autonomous ground vehicles,” in 2022 IEEE International Conference on Autonomous Robot Systems and Competitions (ICARSC). IEEE, 2022, pp. 73–78.
>
> [5] C. Hartsell, N. Mahadevan et al., “Model-based design for cps with learningenabled components,” in Proceedings of the Workshop on Design Automation for CPS and IoT, 2019, pp. 1–9.
>
> [6] I. Malavolta, G. A. Lewis et al., “Mining guidelines for architecting robotics software,” Journal of Systems and Software, vol. 178, p. 110969, 2021. 3
---------------------------------- GUIDELINE CONTENT END ----------------------------------
