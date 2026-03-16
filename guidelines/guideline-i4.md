---
title: "I4. Isolate components for testing"
permalink: /guidelines/guideline-i4
layout: single
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
tags: [isolation, instrumentation, runtime-verification, developer]
---

## Context (WHEN)

> Robotics applications require to be safely field tested with warrantied no side effects on the running system or the environment, including personnel. To this end, it is fundamental to pursue isolation of the components being tested.

Man-in-the-Middle (MITM) can provide isolation of computing nodes for testing, which, as stated by Bertolino et al [1], can guarantee that the execution of the field tests does not interfere with the operation of the tested system. In addition, MITM nodes promotes the ability to drop or modifying internal signals improving the controllability of events and states, which as described by [2], refers to the degree to which a certain specification can be enforced on the system.

```
def instrument_launch_files(nodes):        ...        for (name, package, topics) in launch_files[path]:            if node.get(’name’) == name and node.get(’pkg                ’) == package:                for topic in topics:                    remap = ET.SubElement(node, ’remap’)                    remap.set(’from’, topic)                    remap.set(’to’, topic + ’_mon’)                break
```

## Reason (WHY)

The ROS ecosystem does not provide a native mechanism for node isolation. The MITM node strategy can be a
          powerful and flexible design pattern to isolate computing nodes in ROS-based systems. It allows for increased
          visibility into the system's operation, more flexible communication between nodes, and improved reliability
          and security.

## Suggestion (WHAT)

Isolation of components is an important feature to enable field-based testing (by following the “let it crash” philosophy introduced by Netflix web:chaos-monkey) while avoiding the crash of the system. Isolation permits catching immediately the component that is crashing and executing countermeasures to keep the system up. Examples of solutions for isolation are: (i) the use of proxy nodes of ROSRV (git: cansuerdogan/ROSRV), or (ii) introducing intermediary nodes between original nodes by exploiting the topic remapping functionality (wiki: remap) of ROSMonitoring (git: autonomy-and-verification-uol/ROSMonitoring), which enables swapping topic names just before running the application.

## Process (HOW)

In ROS, the man-in-the-middle (MITM) strategy consists of introducing intermediary ROS nodes between components, in this context the term ‘components’ stands for one or more ROS nodes presenting unique functionality and welldefined interfaces. Such intermediary nodes may react by blocking, dropping, modifying, or inspecting the messages passed between components. We identified two means of enacting MITM in ROS, through a proxy design pattern, e.g., ROSRV [3], or through topic remapping, e.g. ROSMonitoring [4]. The former works by generating a proxy-based of the ROS Master node which has full control of the nodes and topics during runtime, deploying an intermediary node for 1 message diverting when required. The latter launches an intermediary node and performs topic remapping before execution – asking for the topic names that should be diverted.

## Exemplars

#### Proxy

ROSRV[(ROSRV)](https://github.com/cansuerdogan/ROSRV/tree/master/src/RVMaster)[3] deploys a ROS master node proxy, namely RVMaster , that acts as a firewall, blocking the access to the ROS master node port. This node, in turn, is responsible for creating MITM nodes (also called monitors) that intercept the messages flowing between nodes in the system. RVMaster instantiates the MITM nodes according to user-provided specifications of access policies, even though it does not require any change to the system under scrutiny. Listing 1 portrays the createInterceptors () method from the RVMaster that enacts MITM monitor nodes by re-subscribing to a new set of topics.

Listing 1: Creating proxy-based MITM nodes in ROSRV.

```
1. void ServerManager::createInterceptors(){ 
2. 
3. for (std::map<std::string,std::string>::iterator it=rv::monitor:: topicsAndTypes.begin(); it!=rv::monitor::topicsAndTypes.end(); ++it) { 
4. string topic = it->first; 
5. string datatype = it->second; 
6. Monitor *monitor_p = NULL.; 
7. string monitorname = topic+MONITOR_POSTFIX; 
8. 
9. XmlRpc::XmlRpcValue params, result, payload; 
10. params[0] = monitorname; 
11. params[1] = topic; 
12. params[2] = datatype; 
13. string m_uri = ""; 
14. params[3] = m_uri; 
15. 
16. //create a xmlrpcmanager-client for each monitor 
17. monitor_p = new Monitor(params,rv_ros_host, monitorname); 
18. monitorMap[topic] = monitor_p; 
19. m_uri = monitor_p->getMonitorXmlRpcUri(); 
20. params[3] = m_uri; 
21. 
22. bool f = master::execute("registerSubscriber",params,result,payload,true); 
23. 
24. //start a new thread with the params 
25. boost::thread(boost::bind(&Monitor::monitorThreadFunc, monitor_p)); 
26. 
27. result[0]=1; 
28. result[1]="Subscribed to ["+topic+"]"; 
29. XmlRpc::XmlRpcValue pubs_monitor; 
30. pubs_monitor[0] = m_uri; 
31. result[2] = pubs_monitor; 
32. 
33. ROS_INFO("Monitor %s successfully registered a subscriber to topic %s", monitorname.c_str(), topic.c_str()); 2 
34. }
```

#### Topic remapping

Topic remapping. ROSMonitoring[(ROSMonitoring)](https://github.com/autonomy-and-verification-uol/ROSMonitoring)[4] utilizes topic remapping to ensure safety and security in the system by creating intermediary nodes via topic name remapping[(roslaunch/remap)](http://wiki.ros.org/roslaunch/XML/remap). Remapping is a core tool from ROS that enables swapping topic names just before running the application. Remap, enables inserting an intermediary node between the other two original nodes. Listing 2 exemplifies the topic remapping-based MITM strategy applied by ROSMonitoring. The code snippet shows that the launch files are incremented with remap statements including the node names, original (‘from’) topic and new (‘to’) topic name.

Listing 2: Topic remapping-based MITM in ROSMonitoring.

```
1. def instrument_launch_files(nodes): 
2. ...
3. for (name, package, topics) in launch_files[path]: 
4. if node.get(’name’) == name and node.get(’pkg’) == package: 
5. for topic in topics: 
6. remap = ET.SubElement(node, ’remap’) 
7. remap.set(’from’, topic) 
8. remap.set(’to’, topic + ’_mon’) 
9. break
```

Strengths:

The MITM strategy enables freezing of the application at the software level without the normal operation, and
          rollback in case the test scenarios are prone to side-effects and do not require any change in the code.

Weaknesses:

Placing nodes between computations may cause performance overhead in the system under scrutiny. In addition,
          erroneous intermediary nodes may affect the functionality of the system, and thus represent a threat to the
          test's reliability. This guideline does not directly apply to server-based or parameter-based communication.

References

> [1] A. Bertolino, P. Braione et al., “A survey of field-based testing techniques,” ACM Computing Surveys (CSUR), vol. 54, no. 5, pp. 1–39, 2021.
>
> [2] Y. Falcone, S. Krsti´c et al., “A taxonomy for classifying runtime verification tools,” International Journal on Software Tools for Technology Transfer, vol. 23, no. 2, pp. 255–284, 2021. 3
>
> [3] J. Huang, C. Erdogan et al., “Rosrv: Runtime verification for robots,” in International Conference on Runtime Verification. Springer, 2014, pp. 247–254.
>
> [4] A. Ferrando, R. C. Cardoso et al., “Rosmonitoring: a runtime verification framework for ros,” in Annual Conference Towards Autonomous Robotic Systems. Springer, 2020, pp. 387–399.
>
> > ---------------------------------- GUIDELINE CONTENT END ----------------------------------
