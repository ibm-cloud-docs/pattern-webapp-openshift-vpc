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

# Service management design

### **Management and Monitoring**

The recommended approach for multi cluster management and monitoring is to use IBM cloud tools including IBM Log Analysis and IBM Cloud Monitoring. This approach enables application cluster metrics log aggregation and central management within IBM Cloud.

**IBM Log Analysis**

Use IBM Log Analysis to add log management capabilities to Red Hat OpenShift VPC clusters and provide for:

- Customizable user interface for live streaming of log tailing, real-time troubleshooting issue alerts, and log archiving.
- Quick integration with the cluster via a script.
- Aggregated logs across clusters and cloud providers.
- Historical access to logs.
- Highly available, scalable, and compliant with industry security standards.
- Integrated with IBM Cloud IAM for user access management.

**IBM Cloud Monitoring**

Use IBM Cloud Monitoring to monitor the performance and overall system health of Red Hat OpenShift VPC clusters and provide for:

- Customizable user interface for a unified view of cluster metrics, container security, resource usage, alerts, and custom events.
- Quick integration with the cluster via a script.
- Aggregated metrics and container monitoring across clusters and cloud providers.
- Historical access to metrics that is based on the timeline and plan, and ability to capture and download trace files.
- Highly available, scalable, and compliant with industry security standards.
- Integrated with IBM Cloud IAM for user access management.

For more information on how to forward application and cluster metric data to IBM Cloud Monitoring see here: [https://cloud.ibm.com/docs/openshift?topic=openshift-health-monitor\#openshift_monitoring](https://cloud.ibm.com/docs/openshift?topic=openshift-health-monitor#openshift_monitoring)

**Flow Logs for VPC clusters**

Configure IBM Cloud Flow Logs for VPC to gather information about the traffic entering or leaving VPC cluster worker nodes. Flow logs are stored in an IBM Cloud Object Storage instance and can be used for troubleshooting purposes, adhering to compliance regulations. For more information about Flow Logs for VPC, see [Flow logs use cases](https://cloud.ibm.com/docs/vpc?topic=vpc-flow-logs&interface=ui#flow-logs-use-cases).

Using IBM Cloud Monitoring can create alerts when workloads need more resources.

**Resource Management**

Set up spending notifications in IBM Cloud billing. Good practice is to set quotas or resource limits on clusters and namespaces. Cluster administrators make sure that teams that share a cluster don't consume more than their fair share of compute resources (memory and CPU) by creating a [Resource Quota object](https://kubernetes.io/docs/concepts/policy/resource-quotas/) for each Kubernetes namespace in the cluster. If the cluster admin sets a compute resource quota, then each container within the deployment template must specify resource requests and limits for memory and CPU, otherwise the pod creation fails.
