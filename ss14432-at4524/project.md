---
title: "Scheduler for fog computing"
author:
  - Sripranav Suresh Kumar <ss14432@nyu.edu>
  - Abitha Thankaraj<at4524@nyu.edu>
---

For our Big Data and Machine Learning final project we plan to develop a
scheduler for fog/ edge computing.
# Motivation

Fog computing, also called Edge Computing, is intended for distributed computing where numerous 
"peripheral" devices connect to a cloud. With the explosion of IoT devices and widespread availability 
 of internet in the past decade, there has been a push to move computation to devices on the edge. While cloud computing
 offers several advantages wih respect to elasticity and scalability, the distance between the edge devices and
 the cloud gives rise to latency issues. This becomes a bottleneck in IoT applications
 where results to computations are necessary in real-time (like in the case of disaster management
and content delivery applications.) Service Level Agreements (SLAs) may also impose processing at 
locations where the cloud provider does not have data centers. Latency and other limitations have 
been discussed in this [paper](https://www.researchgate.net/profile/Rodolfo-Milito/publication/235409978_Fog_Computing_and_its_Role_in_the_Internet_of_Things/links/0deec531f19946228c000000/Fog-Computing-and-its-Role-in-the-Internet-of-Things.pdf).

Resource management and task scheduling in Fog Computing have garnered interest especially since there has been a
 rise in demand for quality of service in IoT devices. As with the cloud architecture, there cannot be a one size
 fits all solution for scheduling in fog computing. [Matrouk et al.](https://www.atlantis-press.com/journals/ijndc/125951775/view) provide an extensive survey of existing fog schedulers. 
 [Mouradian et al.](https://arxiv.org/pdf/1710.11001.pdf) explores fog computing and enumerates areas of
 further research.

### Scenario

Healthcare has been revolutionised by IoT devices, from making monitoring patient vitals simpler 
to early detection of deadly diseases. We will design a scheduler to detect emergencies in healthcare based on vitals 
monitored by IoT devices. It is crucial that we optimise the device to provide high priority emergencies with timely 
responses.

### Constraints
* The scheduler should be optimised for high priority tasks.
* Scheduling latency should be in the order of milliseconds.

# Proposed Solution

### Tools

[iFogSim](https://github.com/Cloudslab/iFogSim) is a Fog and IoT environments 
simulator dedicated to manage IoT services in a Fog infrastructure. 
We plan to use [iFogSim](https://arxiv.org/abs/1606.02007)
to simulate an IoT setup with fog/edge architecture and come up with our own scheduler.


### Architecture

The edge architecture we propose is a n-level hierarchical architecture which will consist of edge devices like sensors at the 
lowest level and fog devices which perform computation and decision-making at the subsequent higher level. The top level will
eventually be the cloud server where data and records to be stored can be sent and maybe heavy analytics based research can be
done. [HealthEdge](http://www.cs.virginia.edu/~hs6ms/publishedPaper/Conference/2017/HealthEdge-BigData2017.pdf) talks about the 
edge architecture in healthcare systems.

The individual patient level monitoring and welfare assistance will be performed by the fog devices in the intermediate 
levels as quick response(low latency) is paramount. These fog devices will schedule tasks on a priority based approach with 
higher priority for emergency scenarios.

Each of the devices will have its own constraints like their internal processing latency and so on. These 
constraints of the devices will be modelled in the simulator where each of the devices will be assigned specific values for 
the relevant constraints like latency, power usage and so on. 

### Workplan

* Initially, we will set up the simulator and create our edge architecture. This multi level architecture will model the devices on the edge(sensors),
 fog devices and the cloud server.Constraints such as network latency, bandwidth,  and device capacities like CPU power will be enforced by the 
  model on the simulator. The aim of this exercise is to familiarise ourselves with the simulator and with edge architecture. 
  
* Next, we will then work on implementing a naive scheduler
like FCFS, Round-Robin or SJF. While we understand that these algorithms are sub-optimal for our problem, this will 
  allow us to understand custom schedulers in the simulator and give use a baseline for comparison. 

* We will then implement a more intelligent scheduler using our understanding of the constraints and scenarios of our application in edge 
and fog computing. The scenario we want to optimize for is response to emergencies detected by data on vitals sent by devices on the edge.
  Priority and latency will be key parameters for our problem. Since scheduling is a NP Hard problem, we aim to explore heuristics based algorithms for the same.
  
* Finally, we will benchmark the performance of our scheduler against
iFogSim's default scheduler, the naive scheduler we built earlier and other schedulers
that optimize scheduling for similar use cases and constraints.
  

### Evaluation metrics

Our scheduler will be considered successful if it caters to the necessary latency and priority constraints. The scheduling decisions need to 
be completed in the order of milliseconds as in the case of emergencies, response needs to be immediate. However, we will also
compare our scheduler with the default scheduler which is built into iFogSim and the other naive scheduling algorithms.


# Timeline


* Checkin I (03/30): Have iFogSim up and running with a defined edge architecture
    setup. Work on simple scheduler modifications such as FCFS, Round Robin or Shortest job first.
* Checkin II (04/20): We plan to evaluate existing schedulers for edge computing and decide 
on which conditions we will optimise for. 
* Final Handin (05/11): We will have implemented and benchmarked the performance for our scheduler.
