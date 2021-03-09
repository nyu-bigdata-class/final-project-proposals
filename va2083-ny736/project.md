---
title: "Scheduling Algorithm for Clusters with Resource Hogs and Mice"
author:
  - Vinayak Agarwal <va2083@nyu.edu>
  - Neeraj Yadav <ny736@nyu.edu>
---

For our Big Data and Machine Learning final project, we plan to develop a scheduling algorithm for fair resource allocation in systems with resource hogs and mice.

# Motivation

While [Dominant Resource Fairness](http://web.eecs.umich.edu/~mosharaf/Readings/DRF.pdf) provides a pretty fair scheduling algorithm, it falls short in certain scenarios. Consider a scenario where a user requests a really large resource. In such a scenario, the large job may remain starved for a long time because DRF chooses the job with the smallest dominant resource. Consider the Borg scenario itself. 1% of jobs consume 99% of resources. If the jobs were not assigned priorities, and if enough jobs (resource mice) came in every second, the large jobs may not get scheduled at all. DRF hence fails to meet the sharing incentive criteria.

One way we see such a problem get resolved is by looking at [Themis](https://cs.nyu.edu/~apanda/classes/sp21/papers/themis.pdf), where each job is executed for a short span of time before being put back into the queue. This ensures all jobs are executed and no jobs are starved. Themis however considers that most jobs would be resource hogs instead. This may not hold for scenarios as seen in Borg. We need an algorithm that schedules both resource hogs and mice with equal priority while reducing the number of times a job is put back into the queue.

# Proposed Solution

We plan to devise an alternate scheduling algorithm that overcomes the sharing incentive problem as seen in DRF. We take inspiration from Themis, but make the scheduler more suitable to the user pool with varied runtimes. We plan to run simulations on some of the widely used traces (such as the Borg 2019 dataset with all jobs considered equal priority) to test our algorithm's efficiency on parameters such as how many times a job is queued compared to its job execution time and finish-time fairness as seen in Themis.

We are considering using a Hadoop cluster on Cloudlab or Kubernetes to test our scheduling algorithm's performance. If time permits, we would like to extend our algorithm for efficient resource allocation in heterogeneous resources like GPU, FPGA, etc. 

We plan to evaluate our algorithm against the results seen with DRF and Themis, to evaluate how our algorithm performs compared to existing widely used algorithms. If our  algorithm works as intended, it should have a better performance atleast as compared to DRF wrt finish time fairness, and lesser queueing as compared to Themis.

# Timeline

* Check-in I (03/30): Have a well-defined scheduling policy to implement.
* Check-in II (04/20): We plan to have an initial implementation of our scheduling policy. We will have an initial measure of fairness metric.
* Final Hand-in (05/11): Based on preliminary results, we will try to optimize our algorithms, and come up with final evaluation metrics and conclusions.


