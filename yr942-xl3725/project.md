---
title: "Build A Job Scheduler for Clusters based on Reinforcement Learning"
author:
  - Yafu Ruan <yr942@nyu.edu>
  - Xuan Li <xl3725@nyu.edu>
---

For our Big Data and Machine Learning final project we plan to develop a customized scheduler policy using Reinforcement Learning based on an existing paper, <cite>[RLSK: A Job Scheduler for Federated Kubernetes Clusters based on Reinforcement Learning][1]</cite>.

[1]: https://conferences.computer.org/cpsiot/pdfs/IC2E2020-6j9eixwcPIo0tUoMnoCahH/109900a116/109900a116.pdf

# Motivation

The default algorithm of kube-scheduler can help us in most cases, but sometimes people need to develop their own scheduling policy and change the configurations for specific projects in different circumstances. This process involves lots of repeated work done manually to get the optimized solution. To improve the efficiency of the whole process, machine learning models are considered to assist making decisions when scheduling. The status of the clusters and the requirement of the job could be some state features as input, and the model will decide how to allocate the resources to those jobs. A metric will be designed to analyze whether the decision is actually a “good choice”. Reinforcement Learning is one of the models that could explain the problem well.

# Proposed Solution

We plan to construct a Reinforcement Learning model based information from Kubernetes API and job requirements.

* Firstly we design the basic training algorithm using pytorch.
* Next, we will collect resource information from Kubernetes API and transform them to vectors in a proper way. We combine it with job information, which will also be a vector, and take it as the state variable.
* After that, we will design the reward metric to determine how “good” the decision is made by the model. The metric needs to consider the trade-off between the overall utilization and the balance of resources and clusters.
* In the training process, we are going to simulate job loads, whose arrival time, duration and recourses come from certain distributions. This should be similar to the work load simulated in DeepRM as described below(<cite>[Resource Management with Deep Reinforcement Learning][2]</cite>): “jobs arrive online according to a Bernoulli process. The average job arrival rate is chosen such that the average load varies between 10% to 190% of cluster capacity. We assume two resources, i.e., with capacity {1r, 1r}. Job durations and resource demands are chosen as follows: 80% of the jobs have duration uniformly chosen between 1t and 3t; the remaining are chosen uniformly from 10t to 15t. Each job has a dominant resource which is picked independently at random. The demand for the dominant resource is chosen uniformly between 0.25r and 0.5r and the demand of the other resource is chosen uniformly between 0.05r and 0.1r. “ 
* In the testing process, we will try to write a python program to do almost the same and run on k8s(do not sure if it is feasible right now, we will figure it).

We plan to run our experiments on multiple CloudLab nodes.

We will evaluate our work by comparing the performance (average utilization of each cluster) of our scheduling policy with some traditional policy. We will first compare it with Random and Least Load, if we still have time, we will also compare it with round robin.

[2]: https://people.csail.mit.edu/alizadeh/papers/deeprm-hotnets16.pdf

# Timeline


- Checkin I (03/30): We plan to set up the cluster and Kubernetes to let its default scheduling policy run and begin to build the reinforcement learning model using Pytorch based on the paper.
- Checkin II (04/20): We plan to finish building the original model and consider a more suitable neural network model to take more information within the cluster into account.
- Final Handin (05/11): We plan to have the whole scheduler work and compare it with some traditional scheduling policy.