---
title: "Static Code Analysis for Hetrogeneous Cloud Applications"
author:
  - Sriram Ramesh <sriram.ramesh@nyu.edu>
  - Metarya Ruparel <msr9732@nyu.edu>
  - Safwan Mahmood <sm9453@nyu.edu>
---

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

As we are moving towards heterogeneous cloud, we want to write Cloud-Agnostic
applications. To make the transition easier, we propose a static code analyser
to find code snippets specific to a cloud provider using SonarQube Quality
checks. We chose SonarQube as it is widely being used to check for bugs and
code issues in large enterprises. Apart from pointing to the position of the change,
we also provide a correction required to move to a another Cloud provider. 
For example, let us assume that our code analyser checks AWS-specific 
code snippet to move to Azure Cloud. Then, we provide the changes required to move to Azure.

The only way to evaluate our service is to check the accuracy of our recommendations.
We would check the similarity and correctness of our recommended code snippet with the
actual code snippet provided via the cloud service provider (it's no rocket science, to
google a certain part of code).
Example: If we have 4 recommendations, out of which 3 are correct, we can calculate our
accuracy and generate a confusion matrix based on these statistics.

To better explain our hypothesis, let us consider these examples:

As in the case of **batch jobs**, a capability provided by all public clouds, or at least the ones that are
pertinent to the scope of this project.

Usually, batch jobs require spinning up of cluster of workers, followed by jobs submitted to
these workers. When we look at the implementations of this API across all the cloud platforms,
the underlying principle is the same. 

Let's consider a particular case, integration of batch job APIs with Java. Each cloud provider has it's
own library which implements the required functionalities along with required dependencies, such as Maven.
When the library is used, flow across all platforms is the same.

**1. Azure**

The code snipped looks like.

```
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://API.eastus.batch.azure.com", "user", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

While a dependency is being added to pom.xml file.

```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>4.0.0</version>
</dependency>
```

**2. AWS**.

```
public class BatchClient {
public static void main(String[] args) {
        AWSBatch client = AWSBatchClientBuilder.standard().withRegion("us-east-1").build();
SubmitJobRequest request = new SubmitJobRequest().withJobName("example").withJobQueue("new-queue").withJobDefinition("sleep30:4");
SubmitJobResult response = client.submitJob(request);
System.out.println(response);    
}
}
```

While a dependency is being added to pom.xml file.

```
 <!-- https://mvnrepository.com/artifact/com.amazonaws/aws-java-sdk-batch -->
    <dependencies>
    <dependency>
    <groupId>com.amazonaws</groupId>
    <artifactId>aws-java-sdk-batch</artifactId>
    <version>1.11.470</version>
</dependency>
    </dependencies>
```

# Timeline

* Checkin I (03/30): We plan to have our Static Code Analyzer in place which will
  be able to detect cloud dependent code for at least one of the platform providers.
  Example: We will be able to detect that a particular code snippet is meant for job
  scheduling in AWS/Azure.

* Checkin II (04/20): By this time, we will be extending our Static Code Analyzer for
  all the clouds of our interest, i.e, AWS and Azure. We will also have in-place a recommendation
  engine, which would recommend conversions on cloud centric code snippet.
  Example: A code snippet for job scheduling in AWS --> A code snippet for job scheduling in Azure.

* Final Hand-in (05/11): We will have the entire application running end-to-end, from Static Code
  Analyzer to Recommendation Engine which will detect and recommend changes to code snippets which
  are platform centric.
