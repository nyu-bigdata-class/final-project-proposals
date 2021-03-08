---
title: "Extending Redis to support GDPR policy"
author:
  - Kimberly Mishra <km3947@nyu.edu>
  - Rahul Vadaga <srv304@nyu.edu>
---

For our Big Data and Machine Learning final project, we plan to develop a
proxy or middleware to ensure [GDPR](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) compliance with [Redis](https://en.wikipedia.org/wiki/Redis).

# Motivation
As technology has advanced to store and manage big data, consumers and government have become increasingly concerned with regulations on the privacy, sharing, and ownership of data. The General Data Protection Regulation (EU GDPR) seeks to govern data privacy. However, from a systems perspective, translating these articles to capabilities of compliant systems can be a painstaking effort. Moreover, building a system that incorporates all GDPR requirements poses challenges in terms of performance, cost, and reliability. Therefore, extending a storage engine to support all (or at least most of) GDPR requirements and to ensure it meets performance requirements such as storage space overhead, number of transactions per sec, etc. is a problem worth addressing. We seek to research GDPR, make decisions on what is possible to comply with, and build an application that supports this.

GDPR compliance is a problem for both the companies and the users. The users are granted rights but the vagueness of the language in the laws causes a disconnect between which rights are believed to be protected and which truly are. Further, compliance costs are high for businesses. They include systems updates, more storage, and beyond infrastructure changes, failure to comply could result in hefty fines. Without any aid in transitioning toward compliance, smaller companies will be likely to fail quicker than larger ones with more resources at their disposal. Something we found interesting to note is that of the \$63 million in fines issued between the start of GDPR and June 2020, \$57 million were issued to Google.<sup>3</sup>. These problems are further outlined at the resources below:

[1] https://legal.thomsonreuters.com/en/insights/articles/top-five-concerns-gdpr-compliance

[2] https://www.ft.com/content/66668ba9-706a-483d-b24a-18cfbca142bf

[3] https://www.varonis.com/blog/gdpr-effect-review/


# Proposed Solution
We propose to build a proxy/middleware that sits between the data store and application which enforces GDPR compliance. We will create a server that talks to redis through a python or C program. Our program will track and enforce ownership policies and other aspects of GDPR we deem feasible in the research phase of this project. This is further outlined below.

# Timeline

* Checkin I (03/30):
  * **Research on GDPR**:
    * Determine tradeoffs on what parts of GDPR our application can comply with and what is infeasible in the span of a semester. Some of the rights granted to users that we plan to explore include:
      - [ ] Right to access.
      - [ ] Right to rectification.
      - [ ] Right to be forgotten.
      - [ ] Right to object.
      - [ ] Right to data portability.
    * Some responsibilities the companies are given in GDPR that we will explore are:
      - [ ] Seeking consent before using personal data.
      - [ ] Notifying data breaches within 72 hours of discovery.
      - [ ] Maintaining records of processing activities.
  * **Formally define** the scope of our application:
    * What parts of GDPR we will comply with, and what we choose to leave out.
  * **Begin building the architecture** of our solution sketched above using the decisions and research outlined in previous bullets.
    * Have a simple server (using Flask/Django) that relies Redis to store user's data.
    * We'll also create a script using the Python requests library that talks to the server to simulate client-server communication.


* Checkin II (04/20):
  * Define the APIs required to be supported by the middleware. Implement to some extent the API layer, and start making changes to the server design to use this layer for storing and reading data.
  * Specify what metrics we will be evaluating on.


* Final Handin (05/11):
  * Complete implementation of middleware/proxy.
  * Complete evaluation using benchmarks such as GDPRBench.
  * Decisions on various algorithms to use in order to both comply with GDPR and improve performance.
  * Comprehensive documentation of compliance and limitations of our service.
    * Give numeric values and comprehensive reports to vagueness described in GDPR (i.e. if GDPR says you have the right to have your data forgotten in a timely manner, how long does it take us to "forget" your data and what exactly are we "forgetting"?)
    * What parts did we chose to leave out?
      * Why did we decide to leave them out?


#### Sources ####
[1] [EU GDPR](https://gdpr-info.eu/)

[2] [Comparing privacy laws: GDPR v. CCPA](https://fpf.org/wp-content/uploads/2018/11/GDPR_CCPA_Comparison-Guide.pdf)

[3] [Top five concerns with GDPR compliance](https://legal.thomsonreuters.com/en/insights/articles/top-five-concerns-gdpr-compliance)

[4] [EU admits it has been hard to implement GDPR](https://www.ft.com/content/66668ba9-706a-483d-b24a-18cfbca142bf)

[5] [A Year in the Life of the GDPR: Must-Know Stats and Takeaways](https://www.varonis.com/blog/gdpr-effect-review/)

[6] Understanding and Benchmarking the Impact of GDPR on Database Systems
    [[Paper]](https://arxiv.org/pdf/1910.00728.pdf)
    [[Slides]](https://04e19274-9945-4166-b1be-95d42dc718a3.filesusr.com/ugd/13b079_4887efca8131475a93b05048804fe0d4.pdf)

[7] [GDPRBench](https://www.gdprbench.org/benchmark)

