---
title: "I3. Provide an API for injecting faults in execution scenarios"
permalink: /guidelines/guideline-i3
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Context (WHEN)

> Stimulating ROS-based systems with unexpected scenarios is a cornerstone of gathering confidence in the system’s robustness [1, 2]. Such unexpected scenarios either emerge from faults in the robot’s control logic or unforeseen inputs unfolding from complex interactions with the environment. Therefore, preparing the ROS-based systems to systematically explore unintended behavior and complex environmental interactions becomes important in runtime verification [3] and field-based testing [4] for robust ROS-based applications. Fault injection and error emulation are the two fundamental approaches to systematically stimulating a computing system with unexpected scenarios for confidence-gathering purposes [5].

## Reason (WHY)

Providing an API for stimulating unexpected scenarios for testing the robustness of the target system can help address challenges in finding both fault and error sets representative of real software faults.

## Suggestion (WHAT)

To enable runtime verification and field-based testing, developers should provide an API for injecting faults or emulating runtime errors. For instance, to emulate the consequences of software faults, ros1-fuzzer (git:[aliasrobotics/ros1_fuzzer](https://github.com/aliasrobotics/ros1_fuzzer)) provides an API for ROS messages fuzzing. As another example, to imitate the mistakes of programmers, IM-FIT (git:[cembglm/imfit](https://github.com/cembglm/imfit)) is a tool for injecting faults in ROS applications.

## Process (HOW)

There are two identified means to enabling unexpected scenarios injection in ROS: providing an API fault injection and or an API for error emulation. The two methods differ concerning their assumptions. Fault injection is about changing the source code and requires knowledge about the system’s internal structure (e.g., imfit [6]). Error emulation is about changing the system during execution and should not require knowledge about the system itself (e.g., ros1 fuzzer, and ros2 fuzzer). Thus, from the developer’s point of view, enabling faulty scenarios through an API requires deciding whether fault injection or error emulation is the most suitable based on the system’s requirements.

## Exemplars

#### Fault injection

Fault injection imitates the mistakes of programmers by changing the system under scrutiny’s source code [7]. Developers can embed an interface for enabling source code modifications to inject faults in the ROS-based system. For instance,[IM-FIT](https://github.com/cembglm/imfit)is a tool tailored to mutation-based software fault injection for ROS applications [6]. Listing 1 describes a subset of the IM-FIT ROS mutations library which offering three operations (delete, change, and external) on defined ROS primitives, such as publishers, subscribers, timers, global variables, namespaces, service clients. Moreover, IM-FIT offers an interface to decide when, where and how the mutators will inflict faults in the source code. Embedding IM-FIT in the project as an API to fault injection facilitates robustness testing for the QA team.

Listing 1: Snippet of the IM-FIT’s JSON library containing mutations for fault injection in ROS-based systems.

```
1. {"all_faults": [ 
2. {"fault": { 
3. "Fault_Name": "Subscriber Delete", 
4. "Target_to_Change": "rospy.Subscriber", 
5. "Changed": " ", 6 "Explanation": "Subscriber deletes" 
7. }}, 
8. ... 
9. {"fault": { 
10. "Fault_Name": "Periodic Timer Change", 
11. "Target_to_Change": "rospy.Timer", 
12. "Changed": "rospy.Time", 
13. "Explanation": "Periodic timer is wrong" 
14. }}, 
15. ... 
16. {"fault": { 
17. "Fault_Name": "External ROS Message", 
18. "Target_to_Change": "[rospy.Message]{13}", 
19. "Changed": "rospy.Message rospy.Message", 
20. "Explanation": "External ROS Message"" 
21. }} 
22. ]}
```

#### API for error emulation

Error injection attempts to emulate the consequences of software faults by manipulating the runtime states/events of the system under scrutiny [8]. Developers can embed an interface within the ROS-based system enabling a set of operations to disturb it during runtime. For instance,[ros1-fuzzer](https://github.com/aliasrobotics/ros1_fuzzer)provides an API for ROS messages fuzzing. The API requests the topic’s name, the message type and datatype strategies to fuzzing the message’s content. Although the datatype and constraints are hard coded in the API, defining the topic name and message type are done in the command line. For example, $ ros_fuzzer -t / rosout -m rosgraph_msgs / Log, in which the user is fuzzing a Log message sent to the / rosout topic. The 2 authors evolved ros1-fuzzer to suit ROS 2 applications, resulting in[ros2-fuzzer](https://github.com/aliasrobotics/ros2_fuzzer). ros2-fuzzer extends the interface enabling servicelevel fuzzing, not only message fuzzing as was ros1-fuzzer. The addition affected the API asking for an extra argument (service or message) in the command, e.g., $ ros2_fuzzer .py service example_interfaces / AddTwoInts add_two_ints.

Strengths:

Providing an API for fault injection and error emulation with a representative set of possible operations enables black-box robustness testing. It also may save time for the testing team, which can build scenarios on top of the provided interface.

Weaknesses:

Embedding an interface for enabling source code modifications or runtime disturbances can be time-consuming for developers whenever there are no third-party tools that provide the required operations. This guideline should be avoided when verifying or testing safety-critical systems.

References

> [1] A. Afzal, C. Le Goues et al., “A study on challenges of testing robotic systems,” in 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020, pp. 96–107.
>
> [2] C. Hutchison, M. Zizyte et al., “Robustness testing of autonomy software,” in 2018 IEEE/ACM 40th International Conference on Software Engineering: Software Engineering in Practice Track (ICSE-SEIP). IEEE, 2018, pp. 276–285.
>
> [3] Y. Falcone, S. Krsti´c et al., “A taxonomy for classifying runtime verification tools,” International Journal on Software Tools for Technology Transfer, vol. 23, no. 2, pp. 255–284, 2021.
>
> [4] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [5] J. A. Duraes and H. S. Madeira, “Emulation of software faults: A field data study and a practical approach,” Ieee transactions on software engineering, vol. 32, no. 11, pp. 849–867, 2006.
>
> [6] U. Yayan and C. Baglum, “Tailored mutation-based software fault injection tool (im-fit),” SoftwareX, p. 101463, 2023.
>
> [7] R. Barbosa, J. Karlsson et al., “Fault injection,” Resilience Assessment and Evaluation of Computing Systems, pp. 263–281, 2012. 3
>
> [8] R. K. Lenka, S. Padhi et al., “Fault injection techniques-a brief review,” in 2018 International Conference on Advances in Computing, Communication Control and Networking (ICACCCN). IEEE, 2018, pp. 832–837. 4
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
