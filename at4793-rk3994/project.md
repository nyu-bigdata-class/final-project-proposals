---
title: "Kubernetes monitoring tools and techniques: A detailed analysis"
author:
  - Aakriti Talwar<at4793@nyu.edu>
  - Ramneek Kaur <rk3994@nyu.edu>
---


For our Big Data and Machine Learning final project we plan to present a deep dive analysis and comparison between top monitoring and reporting open source solutions available for Kubernetes clusters.

# Motivation

The DevOps conceptual practice forces us to break significant problems into smaller problems. Microservices fit perfectly here, where small services build-up a component, and these components make up an application. The microservice architecture utilizes small teams to develop functional components one by one. By using a microservice architecture, it’s easy to make it faster, scale up and down without impacting the whole system. It’s also better for fault tolerance and is platform and language agnostic. Everything has pros and cons and for microservice architecture, it’s hard to maintain testing and monitoring.

In microservice architecture, we deploy microservices as a container and for orchestration of containers, we rely heavily on tools like Kubernetes or Docker Swarm. Once deployed, microservice architecture has thousands of services talking to each other through networking, which can make it very challenging to monitor. We have to monitor independent services more than service to service communication. Kubernetes is widely growing in the market and it has a large rapidly growing ecosystem. Over the time many organizations are investing their resources in Kubernetes. Since it is open source, there are numerous plugins and tools available for analysis and reporting of the clusters. There are no definite comparisons between all of these tools and plugins available and neither do these organisations have time and resources to explore each of them individually. 

Resources Used:
https://logz.io/blog/kubernetes-monitoring/

# Proposed Solution
* Firstly, we will set up a working 3 node kubernetes cluster.
* Second, we plan to run varying workloads on the cluster.
* Third, we will implement the few widely known tools individually.
* At last, we aim to analyse and compare all the tools based on the following parameters:
  * Ease of implementation.
  * User Experience.
  * Level of monitoring available: cluster level, node level and pod level.
  * The time at which the user is notified before a potential failure.
  * Maintenance Schedules
  * Configuration ease with different setups.
* We will evaluate our progress by comparing the analysis of the tools on different workloads and failure scenarios. We would then provide a detailed report of the behaviour of these tools in the above conditions.   


# Timeline

* Checkin I (03/30): We plan to  setup Kubernetes cluster with minimum workload and than we would devise a solution to vary the amount of workload on the cluster. 
* Checkin II (04/20): Implementation of all the tools on the cluster should be done by this checkin point.
* Final Handin (05/11): We plan to prepare a detailed paper of the analysis of different tools with varying workload on the basis of above mentioned parameters.



