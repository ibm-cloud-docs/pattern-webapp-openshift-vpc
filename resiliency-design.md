---
copyright:
  years: 2024
lastupdated: "2024-04-29"

subcollection: pattern-webapp-openshift-vpc
keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Resiliency design
{: #resiliency-design}

High availability is built into IBM Cloud VPC Red Hat OpenShift clusters and can be increased to meet availability requirements. To increase availability, consider deployment strategies for the number of nodes within a cluster and the node placement within a cluster across availability zones.

## Cluster planning for high availability
{: #cluster-planning-ha}

Users are less likely to experience downtime when apps are distributed across multiple worker nodes, zones, and clusters. Built-in capabilities, like load balancing and isolation, increase resiliency against potential failures with hosts, networks, or apps. The following potential cluster setups are ordered with increasing degrees of availability.

### Single zone cluster
{: #single-zone-cluster}

A single control plane running in only one availability zone. To improve application availability and to allow failover if one worker node is not available in the cluster, add additional worker nodes to the single zone cluster. The workload becomes unavailable if there's a zonal outage. Single zone clusters are suitable for only transient or noncritical workloads.

### Multizone cluster
{: #multi-zone-cluster}

Create a multizone cluster to distribute workloads across multiple worker nodes and zones, and protect against zone failures with hosts, networks, or apps. If resources in one zone go down, the cluster workloads continue to run in the other zones. Multizone clusters provide high availability and the following more benefits:

- Easily manage worker nodes of the same flavor (CPU, memory, virtual or physical) with worker pools.
- Guard against zone failure by spreading nodes evenly across the selected multizones and by using anti-affinity pod deployments for applications.
- Decrease costs by using multizone clusters instead of duplicating the resources in a separate cluster.
- Benefit from automatic load balancing across apps with the multizone load balancer (MZLB) that is set up automatically in each zone of the cluster. This was the selected deployment model for the e-commerce use case as it provides the required service level availability and workload management capabilities.

## Cross regional active to active cluster deployment
{: deployment-cross-regional}

For solutions that require high availability and capacity management, two active clusters can be deployed with the workload distributed by using a global load balancer. 
if there's a cluster failure in one region, the second cluster can be scaled to manage the full workload. For the e-commerce use case, it was decided that multiregion deployment was not required with the additional costs factored into the decision.

## Service Level Agreements
{: #sla}

IBM Cloud provides Service Level Agreement eligibility based on these deployment strategies. To meet the Tier 3 SLA of 99.99%, deploy a multizone cluster and distribute the common workload across 2 or more worker in each of three separate Availability Zones for a minimum total of six worker nodes. A Tier 1 SLA of 99.9% is provided for all other configurations including the minimum sizing for single zone and multizone clusters.

For more information, see [IBM Cloud Service Level Agreements](https://www.ibm.com/support/customer/csol/terms/?id=i126-9268&lc=en#detail-document){: external}.
