---
title: "Build A Job Scheduler for Clusters based on Reinforcement Learning"
author:
  - Yafu Ruan <yr942@nyu.edu>
  - Xuan Li <xl3725@nyu.edu>
---

> In what follows instructions (including this one) are in blockquotes, while
> text not in blockquotes is a sample. You should of course replace the title
> author metadata that shows up above with appropriate values.
>
> You should start your proposal by stating a problem statement or an overall
> goal  as below.

For our Big Data and Machine Learning final project we plan to develop a customized scheduler policy using Reinforcement Learning based on an existing paper, <cite>[RLSK: A Job Scheduler for Federated Kubernetes Clusters based on Reinforcement Learning][1]</cite>.

[1]: https://conferences.computer.org/cpsiot/pdfs/IC2E2020-6j9eixwcPIo0tUoMnoCahH/109900a116/109900a116.pdf

# Motivation
> Next you should talk about why, citing sources for your beliefs.

The default algorithm of kube-scheduler can help us in most cases, but sometimes people need to develop their own scheduling policy and change the configurations for specific projects in different circumstances. This process involves lots of repeated work done manually to get the optimized solution. To improve the efficiency of the whole process, machine learning models are considered to assist making decisions when scheduling. The status of the clusters and the requirement of the job could be some state features as input, and the model will decide how to allocate the resources to those jobs. A metric will be designed to analyze whether the decision is actually a “good choice”. Reinforcement Learning is one of the models that could explain the problem well.

# Proposed Solution
> Next you should talk about how you plan to address the problem. 
> This should include information about what infrastructure (e.g., CloudLab
> resources) you plan to use, how you plan to make progress, and how you plan to
> evaluate your view.

We plan to construct a Reinforcement Learning model based information from Kubernetes API and job requirements.

* Firstly we design the basic training algorithm using pytorch.
* Next, we will collect resource information from Kubernetes API and transform them to vectors in a proper way. We combine it with job information, which will also be a vector, and take it as the state variable.
* After that, we will design the reward metric to determine how “good” the decision is made by the model. The metric needs to consider the trade-off between the overall utilization and the balance of resources and clusters.

We plan to run our experiments on multiple CloudLab nodes.

> You should also talk about how you will evaluate your progress, and what you
> think the ideal end goal would look like.

We will evaluate our work by comparing the performance (average utilization of each cluster) of our scheduling policy with some traditional policy, like Least Load, Round Robin and Random.

# Timeline
> You should lay out a plan for what you hope to have done by each checkin. Note
> we understand that sometimes unexpected bugs or other problems lead to slip
> ups, but the idea behind the timeline is to provide you with the ability to
> determine where you are in this process. It is important you propose a
> realistic timeline that accounts for classes, interviews and other things
> going on in your life.

- Checkin I (03/30): We plan to set up the cluster and Kubernetes to let its default scheduling policy run and begin to build the reinforcement learning model using Pytorch based on the paper.
- Checkin II (04/20): We plan to finish building the original model and consider a more suitable neural network model to take more information within the cluster into account.
- Final Handin (05/11): We plan to have the whole scheduler work and compare it with some traditional scheduling policy.