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

For our Big Data & Machine Learning final project we plan to hypothesize a solution
for Interoperability in the Heterogeneous Cloud Environment, a blatant issue 
industry wide.

# Motivation

After the burst of cloud platforms in 2006 with the introduction of Amazon
Web Services, a lot of companies started migrating their services to the 
cloud platform from a bare metal lying in one of their own datacenters.
Big hulking datacenters are a necessary evil, a barely concealed secret. 
No one wants to build one. They’re certainly impressive – they resemble the 
set of a science fiction movie, row upon row of silent machines. But they’re 
wildly expensive, and their maintenance challenges are never ending. 

Cloud Platforms provided these companies the ability to access shared, online computing 
resources, without the over head of maintaining them. However, these providers often 
offer their own proprietary applications, interfaces, APIs and infrastructures, which
somewhat makes these providers unique. Due to the uniqueness (be it performance or costing)
companies would want to onboard different set of services onto various providers.
For example, Salesforce.com, which  started the wave of SaaS back in the late 1900's 
, has only recently started it's migration from 1st party datacenters to these 3rd party
providers. Some of their micro-services are being on-boarded to GCP, while a couple of
others to AWS, resulting in a heterogeneous cloud environment. This heterogeneous 
environment makes it difficult for companies to change cloud service providers; in 
any case. Exploring capabilities to support the automated migration from one provider 
to another is an active, open research area. A lot of people have been pursuing approaches 
to reduce the impact of vendor lock-in by investigating the cloud migration problem 
at the level of the VM. However, the migration downtime, decoupling VM from
underlying systems and security of live channels remain open issues and as a part of
this project we aim to hypothesize a solution to at least one blatant issue in the
process of migration.

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
