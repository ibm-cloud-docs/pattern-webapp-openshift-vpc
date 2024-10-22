---
copyright:
  years: 2024
lastupdated: "2024-05-02"

subcollection: pattern-webapp-openshift-vpc

keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Compute design
{: #compute-design}

The following are the compute design considerations based on the Red Hat OpenShift on {{site.data.keyword.vpc_full}} pattern.

![Compute design for web application deployment](image/Merged_Reference_OpenShift-ComputeDesign.drawio.svg){: caption="Compute design for web application deployment" caption-side="bottom"}

1. A VPC Landing Zone is deployed which provides the ability to automate the installation of an Red Hat OpenShift cluster into a multizone region.
2. Three separate clusters are created for the production, pre-production, and dev and test environments. The diagram depicts only the production cluster.
3. Separate worker pools are created within the clusters for the application and storage workloads.
4. The worker pool node size and quantity are determined based on the resource requirements for the application and storage workloads.
5. To meet the Red Hat OpenShift on VPC service availability Service Level Agreement (SLA) of 99.99%, a minimum of 6 worker nodes are equally distributed across three availability zones.
6. Total worker node capacity is sized at 150% of the total workload's required capacity, so that if one zone fails, the resources are available to maintain the workload.
7. By default, the cluster is provisioned with a VPC security group and a cluster-level security group.
8. The Red Hat OpenShift platform is integrated with {{site.data.keyword.Bluemix_notm}}d Services to provide centralized cluster observability services.

## Capacity planning for your Red Hat OpenShift cluster
{: #capacity-planning-red-hat}

It's important to plan for the expected capacity of the Red Hat OpenShift deployment to ensure proper infrastructure size and resource availability. The capacity planning should address current needs and future growth. Worker nodes in a worker pool can easily be added and removed in response to changing workload demands. The capacity change process can be automated by using [autoscaling](/docs/openshift?topic=openshift-cluster-scaling-classic-vpc) for the VPC cluster. The cluster-autoscaler add-on can scale the worker pools in the VPC cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing needs of scheduled workloads. When determining worker node and cluster size and deployment strategy consider the following workload requirements and enterprise business needs:

- The infrastructure view including compute (CPU, memory, and disk capacity), storage, and network requirements.
- Service, usability, and application view, which can include middleware, databases, applications, data persistency and high availability.
- Workload behavior patterns and forecasts can include: seasonal peaks for workloads, and event-driven increases such as market campaigns, mergers and acquisitions, and new project deployment.
- Consider Service Level Agreements (SLAs), high availability, resiliency, and disaster recovery requirements

## Sizing your Red Hat OpenShift cluster environment
{: #sizing-your-environment}

### Determining the number of clusters required
{: #determining-cluster-size}

- The number of ROKS clusters is decided based on the number of environments.
- For this use case, we have 3 environments. Dev/Test, Pre-Production, and Production. So, the decision is to have 3 Red Hat Openshift clusters.
  - 1 for Dev/Test environment separated by Red Hat OpenShift projects. Merging nonproduction into a single cluster is valid in any scenario where a reduction in the infrastructure and management costs is required.
  - 1 for Pre-Production Environment.
  - 1 for the Production environment.

### Determine the workload and resource requirements for your environment

The following general resource consumption guidance for common microservice workloads can also be considered:

- Node.js: 1.5 to 2.5 vCPU average consumption per production application with an average TPS of 1000 and three replicas.
- Java: 2.5 to 4.5 vCPU average consumption per production application with an average TPS of 1000 and three replicas.

For any additional workloads like the integrated services, OEM services, and add-on workloads, additional cluster resources are required. The sizing needs to be planned by working with the third-party vendor and it must be accounted for in the cluster capacity planning.
{: note}

Also, for stateful applications with shared or persistent storage needs, consider the worker pool requirements for software-defined storage (SDS) solutions such as [Portworx](/docs/openshift?topic=openshift-storage_portworx_about) or [Red Hat OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-storage-prep). A software-defined storage solution abstracts storage devices of various types, sizes, or from different vendors that are attached to the worker nodes in your cluster.

The level of availability set up for the cluster impacts coverage from the [IBM Cloud HA service level agreement terms](/docs/overview?topic=overview-slas).

### Sizing the Red Hat OpenShift cluster environment for the HomeDIY Ltd use case 
{: #sizing-homediy}

In sizing the clusters for the HomeDIY use case, complete the following steps:

1. Determine the workload partitioning strategy and the required number of clusters. For this use case, four environments are in scope and are separated within three Red Hat OpenShift Clusters based on the customer stated business requirements and best practices for environment isolation:
      - Production cluster
      - Pre-production cluster: The Pre-production cluster is being used for load performance testing and needs to mirror the production cluster. This cluster is assumed at 100% of production resources.
      - Nonproduction clusters: The nonproduction environments are being consolidated within a single cluster for operational efficiency and are being isolated within separate namespaces to define specific user access and roles.
        2. User acceptance testing is assumed at 50% of production resources.
        3. Development is assumed at 25% of production resources.

Use case sizing decision:
- Three Red Hat OpenShift clusters: (1) Production, (2) pre-production, and (3) dev and test

2. Determine the workload resource requirements for environments. 
   1. Calculate the resource requirements for the in scope environments based on the average transactions per second expected in production for the ecommerce application solution.
   2. There are 20 microservices supporting a web with an average API load of 750 Transactions Per Second (TPS) and mobile channel with an average API load of 1000 TPS.
   3. A typical Node.js application with three replicas averaging 1750 TPS can minimally be expected to consume between 2.5 and 4.5 vCPU as a baseline estimate. The sizing exercise assumes an average utilization of 3.5 vCPU per Node.js application with three replicas.

  Use case sizing decision:

  - Production cluster: 70 vCPU required (20 microservices x 3.5 vCPU)
  - Pre-production cluster: Match to Production
  - Nonproduction cluster: 53 vCPU at 50% of prod which equals 35 vCPU. Dev is 25% of prod which equals 18 vCPU. For the nonproduction environments, assumptions are single replicas with minimal transaction loads.

3. Determine more services included within the cluster.
   1. More services are running within the clusters such as Red Hat OpenShift Service Mesh and IBM Cloud Monitoring agents. For the sizing estimation, assume adding 10% to the e-commerce application worker pool.

  Use case size decision for compute worker pool:

  - Production cluster: 77 vCPU required (70 vCPU \* 1.1)
  - Pre-production cluster: An exact match to production
  - Cluster: 58 vCPU (53 vCPU \* 1.1)

  1. One of the client requirements for the solution is highly available persistent storage. There are stateful applications and a containerized Redis database is being used for event store and message queue purposes.
  2. To meet this requirement, the IBM Cloud [Portworx Enterprise](https://cloud.ibm.com/catalog/services/portworx-enterprise){: external} service is used which provides a software-defined storage solution for the e-commerce workload. A separate worker pool is used for the storage nodes. This allows for disaggregated scaling of the e-commerce worker nodes to meet demand changes that are provisioned for each cluster.
  3. For highly available data storage, Portworx requires at least 3 worker nodes with raw and unformatted block storage.

  Use case size decision for storage worker pool:
  - A separate storage worker pool of three 4 vCPU x 16 GB memory worker nodes is added to the three Red Hat OpenShift clusters.
  
The worker node size represents a minimum worker node flavor for Portworx and specific deployment strategy and sizing is not considered under this pattern.
{: note}

4. Determine the optimal worker node size and quantity for the e-commerce worker pool.
     1. For cost and management optimization, we are choosing 16 vCPU x 64 GB flavor worker nodes.
     2. For pod scheduling and performance considerations, we are limiting the resource available to the application workload to 75% of the work node vCPU capacity.

Use Case Sizing Decision:

  - Production cluster: Seven 16 vCPU x 64 GB worker nodes (16 vCPU (node capacity)) \* 0.75 (reserve capacity) = 12 vCPU. 77 vCPU (compute workload resource requirement) / 12 = 7 (worker nodes rounded up)
  - Pre-production cluster: A match to production
  - Nonproduction cluster: Five 16 vCPU x 64 GB worker nodes (16 vCPU (node capacity)) \* 0.75 (reserve capacity) = 12 vCPU. 58 vCPU (compute workload resource requirement) / 12 = 5 (worker nodes rounded up)

5. Determine your cluster size accounting for resiliency requirements including high availability and SLA targets.
     1. For resiliency we are planning for the total capacity of the production and pre-prod clusters to be at least 150% of the total workload's required capacity, so that if one zone goes down, we have resources available to maintain the workload.
     2. The client availability requirements for the Red Hat OpenShift service availability are 99.99%, which requires our production cluster to have a minimum of 6 worker nodes in a multizone cluster across three availability zones (two worker nodes per AZ). This provides for high availability for the application replicas within an availability zone as well as regionally.

Use Case Sizing Decision:

  - Production cluster: Twelve 16 vCPU x 64 GB worker nodes (7 worker nodes \* 1.5 = 11 and 12 are required to equally distribute across 3 AZs)
  - Pre-production cluster: Match to Production
  - Nonproduction cluster: Six 16 vCPU x 64 GB worker nodes (5 worker nodes and 6 are required to equally distribute across 3 AZs)

A minimum of 6 worker nodes that are equally distributed across three availability zones is required to meet the Cloud Service Level Agreement of 99.99% for Tier 3 (High Availability) and for the HomeDIY availability SLA requirement to be met.
{: note}

6. Putting it all together to determone the final cluster size.

| Cluster and role | Component | Number of worker nodes | Worker node flavor | Cluster type and configuration |
| ------------------------ | ------------------- | ------------------- | ---------------------------- | ------------------------------- |
| 1: Production           | Compute worker pool | 12                  | 16 vCPU x 64 GB Memory       | Multizone: 4 nodes per AZ     |
|                          | Storage worker pool | 3                   | 4 vCPU x 16 GB Memory        | Multizone: 1 node per AZ      |
| 2: Pre-production            | Compute worker Pool |                     | Match to Production          | A match to production             |
|                          | Storage worker pool |                     | Match to Production          | A match to production             |
| 3: Nonproduction             | Compute worker pool | 6                   | 16 vCPU x 64 GB Memory       | Multizone: 2 nodes per AZ     |
|                          | Storage worker pool | 3                   | 4 vCPU x 16 GB Memory        | Multizone: 1 node per AZ      |
{: caption="Final cluster sizing" caption-side="bottom"}

1. Cluster 1: Production
      - Separate worker pools for e-commerce application workload and the software-defined storage layer
1. Cluster 2: Pre-production 
      -  An exact match to production
2. Cluster 3: Nonproduction
      - Single cluster for UAT and dev environments that are separated by the project and namespace
      - Separate worker pools for e-commerce application workload and the software-defined storage layer
