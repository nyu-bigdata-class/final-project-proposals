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

As we are moving towards hetrogeneous cloud, we want to write Cloud-Agnostic
applications. To make the transition easier, we propose a static code analyser
to find code snippets specific to a cloud provider using SonarQube Quality
checks. We chose SonarQube as it is widely being used to check for bugs and
code issues in large enterprises. Apart from pointing to the position of the change,
we also provide a correction required to move to a another Cloud provider. 
For example, let us assume that our code analyser checks AWS-specific 
code snippet to move to Azure Cloud. Then, we provide the changes required to move to Azure.



> You should also talk about how you will evaluate your progress, and what you
> think the ideal end goal would look like.

We will evaluate our project by running a variety of code checks on cloud specific
functions, for instance, like below.

Examples:

Big data, large-scale parallel and high-performance computing applications are been deployed
at higher rates than ever. With burst of such use cases, heterogenous cloud deployment should not
be a bottleneck affecting fast deployments in various public clouds.

We narrow down to a use case of batch jobs, a capability provided by all public clouds, or atleast the ones in 
the scope of our discussion.

Usually, batch jobs require spinning up of cluster of workers, followed by jobs submitted to
these workers. When we look at the implementations of this API across all the cloud platforms,
the underlying principle remains constant. 

Let's consider a particular case, integration of batch job APIs with Java. Each cloud provider has it's
own library which implements the required functionalities along with dependencies required (For example: Maven).
When the library is used, same flow is being executed across all clouds.

Example:

**Azure**

The code snipped looks like.

```
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://API.eastus.batch.azure.com", "user", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

While a dependicy is being added to pom.xml file.

```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>4.0.0</version>
</dependency>
```

Similarly, when we look at **AWS**.

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

While a dependicy is being added to pom.xml file.

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

When we look closely, if such regions are indentified in the code which execute the same common end goal
across the cloud platforms, we could come up with ways to suggest snippets for the targeted cloud. Thus providing the 
same functionality with minimal development overhead.

There are many features across the cloud providers which at core deliver the same functionalities. For the sake of discussion, 
we explore limited examples using clouds like AWS, Azure with Java as targeted language. The use cases can extended across features and languages used.


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
