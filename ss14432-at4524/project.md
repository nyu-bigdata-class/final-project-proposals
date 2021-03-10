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



# Proposed Solution

[iFogSim](https://github.com/Cloudslab/iFogSim) is a Fog and IoT environments 
simulator dedicated to manage IoT services in a Fog infrastructure. 
We plan to use [iFogSim](https://arxiv.org/abs/1606.02007)
to simulate an IoT setup with fog/edge architecture and come up with our own scheduler.

* Initially, we will set up the simulator and create our edge architecture. The aim of this exercise is 
to familiarise ourselves with the simulator and with edge architecture.

* Next, we will then work on implementing a naive scheduler
like FCFS, Round-Robin or SJF. This will allow us to understand custom schedulers in the 
simulator and give use a baseline for comparison. 

* We will then implement a more intelligent scheduler using our understanding of the constraints and scenarios of edge 
and fog computing. (Note: There cannot be a one size fits all solution and 
we will restrict the scenario and the constraints to be optimized for accordingly.)

* Finally, we will benchmark the performance of our scheduler against
iFogSim's default scheduler, the naive scheduler we built earlier and other schedulers
that optimize scheduling for similar use cases and constraints.


# Timeline


* Checkin I (03/30): Have iFogSim up and running with a defined edge architecture
    setup. Work on simple scheduler modifications such as FCFS, Round Robin or Shortest job first.
* Checkin II (04/20): We plan to evaluate existing schedulers for edge computing and decide 
on which conditions we will optimise for. 
* Final Handin (05/11): We will have implemented and benchmarked the performance for our scheduler.
