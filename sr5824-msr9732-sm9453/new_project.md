---
title: "Unsupervised Anomaly Detection in AIOps Lifecycle: A survey of Techniques"
author:
  - Sriram Ramesh <sriram.ramesh@nyu.edu>
  - Metarya Ruparel <msr9732@nyu.edu>
  - Safwan Mahmood <sm9453@nyu.edu>
---

For our Big Data & Machine Learning final project we plan to hypothesize a solution
for **Unsupervised Anomaly Detection in AIOps Lifecycle: A survey of Techniques**

# Motivation

DevOps is a collaborative and multidisciplinary organizational effort
to automate continuous delivery of new software updates while guaranteeing
their correctness and reliability[1].

This methodology for facilitating continutous deployment has been widely
adopted[2]. But the ever-increasing complexity and scale of cloud
computing pose signigicant challenges for operating services with DevOps[3]
which led to introduction of artifiical intelligence to IT operations *AI Ops*[4].

AI Ops tries to be proactive in preventing disasters and helps in root cause 
identification. AIOps finds anomolies in the cluster data by using unsupervised
learning and anomoly detection. There has been techniques has been developed for 
streaming data and benchmarked with real time applications[5].

We want to analyse and benchmark unsupervised learning on the cluster data[6] to 
evaluate the prospects of AIOps in real world usage.

# Proposed Solution

To get the most value out of the AIOps system, it should be deployed as an independent platform that 
ingests data from all IT monitoring sources, and acts as a central system of engagement.

Such a platform must be powered by three major types of algorithms that fully automate and 
streamline three key dimensions of IT operations monitoring:

1. Detection - Machine Learning models trained on past dataset, which would detect any aberration in the
               metrics and would raise a flag. This would be the entry point of the system.
   
2. Triaging - Identifying root causes of problems and recurring issues, so that you can take action 
              on what has been discovered.
   
3. Remediate - Take an appropriate action to avoid/tackle the problem at hand.

These steps occur in a sequential manner, i.e, Once we detect an incident, we triage it and then remediate it.

As part of this project, we are going to deploy the AIOps lifecycle. The way we plan to do this is
as follows:

1. Detection:
    We will have a detection API (Flask application) being served from CloudLab. We will have pre-trained 
    models that would sit on the local file system (we would just pickle them and store them. We are not 
    making it more complex as our main goal is not to have the complete system. Our main goal is to evaluate
    all the different techniques).
   
2. Triage:
    This is the most difficult part to accomplish. We do not plan to come up with a complete RCA. We are 
    going to mock this part with rules, to showcase how all the different parts are stitched together. We
    are going to use StackStorm for this. StackStorm would have sensors, which would poll the data, call 
    our detection API, based on the Anomaly Scores, match a corresponding rule and take an appropriate action.
   
3. Remediate:
    This part contains the set of actions that we would want to take. These actions can be as simple as
    restarting a container. This would again be part of the StackStorm ecosystems. Actions are scripts
    which would be called by StackStorm when a particular rule is matched against it.
   
The reason we want to come-up with the entire AIOps Cycle is to showcase how different detecting algorithms
can have adverse effects in real world. For example: if we miss an incident, there would not be any rules
matched and thus there would not be any action taken on it.

The main part of our project is going to be evaluating different Unsupervised Anomaly Detection Algorithms. 

We plan to serve the following models using the API:

1. Statistical:\
    a. Autoregression (AR)\
    b. Moving Average (MA)\
    c. ARIMA\
    d. SARIMA\
    e. SARIMAX
   
2. Machine Learning Based Models:\
    a. Isolation Forest (ISF)
   
3. Neural Nets:\
    a. LSTM's\
    b. HTM

We will evaluate the above algorithms and study their effects on the AIOps Lifecycle and derive which
one works the best on our dataset.

**Evaluation Metrics:**

We don’t want a scenario where there are alerts raised on false event predictions but also make sure we don't miss out on alert events as False negatives. Our predictions need to have low false positives and along with low false negatives.

**Accuracy:**
A common metric to evaluate performance of a model. In our case, where anomaly is an rare event compared to the rest, accuracy doesn't give a sound picture because of imbalanced classes.
The chances of actually having anomaly are very low. Let’s say out of 100, 90 of the events don’t have anomaly and the remaining 10 actually have it. We don’t want to miss on an event which is having an anomaly but goes undetected (false negative). Detecting every event as not having anomaly gives an accuracy of 90% straight. The model did nothing here but just gave anomaly free for all the 100 predictions.

**Precision:**
Gives percentage of positive instances out of the total predicted positive instances. Take it as to find out ‘how much the model is right when it says it is right’.

So high precision is one such desired metric.

**Recall:**
Take it as to find out ‘how much extra right ones, the model missed when it showed the right ones’.
We aim for low recall.

**F1 score:**
Combines precision and recall. Higher the F1 score, the better.
So a model does well in F1 score if the positive predicted are actually positives (precision) and doesn't miss out on positives and predicts them negative (recall).

Like in our case, which has a high class imbalance because very few have anomalies out of all the events. We certainly don’t want to miss on an event having anomaly and going undetected (recall) and be sure the detected one is having it (precision).

F1 score is an apt metric evaluation for our use case.

**Others evaluation metrics:**
* Confusion matrix
* Logarithmic Loss
* Area under curve (AUC) (The nonparametric use of ROC curves for computing AUC values)

**Regression metrics:**
* Root Mean Squared Error
* Mean Absolute Error.


# Timeline

* Checkin I (03/30): We plan to complete the evaluation of all the statistical models.

* Checkin II (04/20): We plan to deploy all the models on CloudLab and serve them via API. 
  We will also start with StackStorm and have the sensor ready to poll data and call the API.

* Final Hand-in (05/11): We will have the complete evaluation of all our Anomlay Detection Model and 
  also a complete AIOps Lifecycle (using StackStorm) to study the effect of these algorithms on real world systems.
  
# References
1. https://arxiv.org/pdf/1909.05409.pdf
2. G. Kim, P. Debois, et al, “The DevOps Handbook: How to Create WorldClass Agility, Reliability, and Security in Technology Organizations”, IT
Revolution Press, Oct. 2016
3. https://ieeexplore-ieee-org.proxy.library.nyu.edu/stamp/stamp.jsp?tp=&arnumber=8802836
4. https://www.moogsoft.com/resources/aiops/guide/everything-aiops/
5. https://www.sciencedirect.com/science/article/pii/S0925231217309864
6. https://github.com/alibaba/clusterdata
7. https://github.com/StackStorm/st2

