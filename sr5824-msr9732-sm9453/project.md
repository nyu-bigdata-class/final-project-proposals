---
title: "Static Code Analysis for Hetrogeneous Cloud Applications"
author:
  - Sriram Ramesh <sriram.ramesh@nyu.edu>
  - Metarya Ruparel <msr9732@nyu.edu>
  - Safwan Mahmood <sm9453@nyu.edu>
---

> In what follows instructions (including this one) are in blockquotes, while
> text not in blockquotes is a sample. You should of course replace the title
> author metadata that shows up above with appropriate values.
>
> You should start your proposal by stating a problem statement or an overall
> goal  as below.

For our Big Data and Machine Learning final project we plan to develop a
static code analyser for applications targeting hetrogeneous cloud environment.

# Motivation
> Next you should talk about why, citing sources for your beliefs.

Recently, there has been a lot of excitement around quantum computing, and in the
last three years [Google](https://www.nature.com/articles/s41586-019-1666-5),
[Microsoft](https://azure.microsoft.com/en-us/solutions/quantum-computing/) and
others have begun to demonstrate that we are getting close to the point where we
can feasibly build and run programs on quantum computers. A lot of the
excitement around quantum computing stems from its ability to solve some
problems exponentially faster than classical computers. However, all current
quantum computers have limited memory resources, mostly only a few qubits.
Therefore, actual applications are likely to require resources across multiple
quantum computers, but this problem has not been considered thus far.

# Proposed Solution
> Next you should talk about how you plan to address the problem. 
> This should include information about what infrastructure (e.g., CloudLab
> resources) you plan to use, how you plan to make progress, and how you plan to
> evaluate your view.

As we are moving towards hetrogeneous cloud, we want to write Cloud-Agnostic
applications. To make the transition easier, we propose a static code analyser
to find code snippets specific to a cloud provider using SonarQube Quality
checks. Apart from pointing to the position of the change, we also provide
a correction required to move to a another Cloud provider. For example, let us
assume that our code analyser checks AWS-specific code snippet to move to
Azure Cloud. Then, we provide the changes required to move to Azure.

We chose to implement this as an extension of existing SonarQube infrastructure
to ease the integration of the tool.

> You should also talk about how you will evaluate your progress, and what you
> think the ideal end goal would look like.

We will evaluate our project by running a variety of circuits both large and
small. We will use large circuits to demonstrate that our approach makes some
computations feasible, while we will use small circuits (which can be run on
both a single instance and distributed) to measure the performance overhead.

# Timeline
> You should lay out a plan for what you hope to have done by each checkin. Note
> we understand that sometimes unexpected bugs or other problems lead to slip
> ups, but the idea behind the timeline is to provide you with the ability to
> determine where you are in this process. It is important you propose a
> realistic timeline that accounts for classes, interviews and other things
> going on in your life.

* Checkin I (03/30): Have QX and ScaffCC running, have a large circuit that
    cannot be run on one machine, and a manual partitioning where each part can
    be run on a machine.
* Checkin II (04/20): We plan to have an initial implementation where multiple
    Qx instances can communicate with each other. We will have an initial
    measure of performance overheads. We also plan to have decided whether and
    how to optimize our implementation to reduce these overheads.
* Final Handin (05/11): We will have the distributed implementation, and an
    initial system that uses heuristics to partition the circuit.
