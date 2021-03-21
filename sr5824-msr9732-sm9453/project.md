---
title: "Project Title"
author:
  - Paddington Bear <bear@paddington.com>
  - John Appleseed <ja@example.com>
---

> In what follows instructions (including this one) are in blockquotes, while
> text not in blockquotes is a sample. You should of course replace the title
> author metadata that shows up above with appropriate values.
>
> You should start your proposal by stating a problem statement or an overall
> goal  as below.

For our Big Data and Machine Learning final project we plan to develop a
framework for writing distributed quantum computing applications.

# Motivation
> Next you should talk about why, citing sources for your beliefs.

Recently there has been a lot of excitement around quantum computing, and in the
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

Since quantum computers are not easily accessible at the moment, we plan to
rely on the [Qx](http://qutech.nl/qx-quantum-computer-simulator/) simulator, and
build on the work done in [ScaffCC](https://github.com/epiqc/ScaffCC). Currently
QX can only simulate O(10) qubits and hence closely matches our assumptions
above. Our plan then proceeds as follows:

* We plan to start by creating large circuits in ScaffCC, building test programs
that cannot be simulated using Qx. 
* Next, we will partition these circuits by hand into portion that can be run on
  individual Qx instances. 
* Next, we will develop a wrapper around Qx so that results from one instance
    can be communicated to another. We will use this wrapper to assemble the
    individual pieces of the circuit into one program and show that we can
    compute the entire program.
* Next, we plan to work on developing techniques to automatically partition code
  circuits rather than hand partitioning them. We will begin by developing
  simple heuristics for this, and extend if time allows.

We plan to run our experiments on multiple CloudLab nodes, each of which
executes one instance of QX.

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
