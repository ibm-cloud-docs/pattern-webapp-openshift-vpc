---
copyright:
  years: 2024
lastupdated: "2024-04-11"

subcollection: pattern-webapp-openshift-vpc
keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Resiliency design

{: #resiliency-design}

Please see the VPC resiliency architecture pattern \<here\>

High availability is built into IBM Cloud VPC Red Hat OpenShift clusters and can be increased to meet availability requirements. To increase availability, consider deployment strategies for the number of nodes within a cluster and the node placement within a cluster across availability zones.

**Cluster planning for high availability**

Users are less likely to experience downtime when apps are distributed across multiple worker nodes, zones, and clusters. Built-in capabilities, like load balancing and isolation, increase resiliency against potential failures with hosts, networks, or apps. The following potential cluster setups are ordered with increasing degrees of availability.

**Single zone cluster:**

A single control plane running in only one availability zone.

To improve application availability and to allow failover in the event that one worker node is not available in the cluster, add additional worker nodes to the single zone cluster.

The workload becomes unavailable in the event of a zonal outage. Suitable for transient or non-critical workloads only.

**Multizone cluster:**

Create a multizone cluster to distribute workloads across multiple worker nodes and zones, and protect against zone failures with hosts, networks, or apps. If resources in one zone go down, cluster workloads continue to run in the other zones.

Multizone clusters provide high availability and the following additional benefits:

- Easily manage worker nodes of the same flavor (CPU, memory, virtual or physical) with worker pools.
- Guard against zone failure by spreading nodes evenly across the selected multizones and by using anti-affinity pod deployments for applications.
- Decrease costs by using multizone clusters instead of duplicating the resources in a separate cluster.
- Benefit from automatic load balancing across apps with the multizone load balancer (MZLB) that is set up automatically in each zone of the cluster. This was the selected deployment model for the E-commerce use case as it provides the required service level availability and workload management capabilities.

**Cross Regional Active-Active Cluster deployment**

For solutions requiring high availability and capacity management, 2-active clusters can be deployed with the workload distributed using a global load balancer. In the event of a cluster failure in one region the second cluster can be scaled to manage the full workload.

For the E-commerce use case it was decided multi region deployment was not required. The additional costs factored into th decision.

**Service Level Agreements**

IBM Cloud provides Service Level Agreement eligibility based on these deployment strategies.

To meet the Tier 3 SLA of 99.99%, deploy a multizone cluster and distribute the common workload across 2 or more worker in each of three separate Availability Zones for a minimum total of six worker nodes. A Tier 1 SLA of 99.9% is provided for all other configurations including the minimum sizing for single zone and multizone clusters.

[For more information, see IBM Cloud Service Level Agreements.](https://www.ibm.com/support/customer/csol/terms/?id=i126-9268&lc=en#detail-document)
