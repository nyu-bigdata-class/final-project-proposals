---
title: "MEAN stack vulnerabilities diagnose with Kubernetes monitoring tools"
author:
  - Aakriti Talwar<at4793@nyu.edu>
  - Ramneek Kaur <rk3994@nyu.edu>
---

For our Big Data and Machine Learning final project we plan to use cAdvisor, Jaeger, Graylog and Grafana as kubernetes monitoring tools to diagnose commonly faced performance issues for MEAN stack applications.

# Motivation

Using microservice architecture like kubernetes makes it easier and faster to scale applications without impacting the whole system and hence is a widely growing ecosystem. Since microservice architecture has numerous services talking to each other, monitoring applications becomes a challenging task.

MEAN stack is a popular javascript based open source full stack framework that includes MongoDB, Express.js, Angular.js and Node.js used  to create dynamic, fast, and secure websites and web applications that scale. This framework is although pretty flexible and powerful comes with its own set of difficulties. Some common problems faced by MEAN stack applications are:
* Uncaught exception or error event in JavaScript code
* Unresponsive application, possibly looping or hanging
* Excessive memory usage, which may result in an out-of-memory error
* Heavy weight computation causes poor performance.
* Cross-site scripting attack.
* SQL injection type attacks.

So in scenarios where these MEAN Stack applications are running on Kubernetes clusters it becomes all the more difficult to diagnose the above mentioned problems. Our goal is to use four different monitoring tools namely, cAdvisor, Jaeger, Graylog and Grafana to monitor and find out which out of these can provide the most accurate metric for fast diagnosis of the above mentioned issues which would in turn lead to shorter issue resolution time.


Resources Used:
https://www.mongodb.com/mean-stack
https://www.upguard.com/blog/full-stack-blues-exploring-vulnerabilities-in-the-mean-stack
https://logz.io/blog/open-source-monitoring-tools-for-kubernetes/

# Proposed Solution

* Firstly, we will set up a working 3 node kubernetes cluster.
* Second, we plan to build a Blog website using MEAN stack and package to run it on the Kubernetes cluster.
* Third, we will implement the above mentioned monitoring tools individually.
* Fourth, we will induce the above mentioned problems one by one.
* Next for each scenario  we will check how accurately each tool or a combination of these tools  is able to diagnose the problem.


* We will evaluate our progress by inducing problem scenarios for our MEAN stack application and then evaluating the metrics provided by each tool at that particular timestamp to check how accurately we are able to catch the real reason behind the performance issue. 


# Timeline

* Checkin I (03/30): We plan to build Blog CMS application using mean stack . 
* Checkin II (04/20): Setup Kubernetes and install all the above mentioned monitoring tools.
* Final Handin (05/11): We plan to prepare a detailed paper with the experiment results of how useful each monitoring tool was for diagnosing the problem scenarios induced for our MEAN Stack Application.


