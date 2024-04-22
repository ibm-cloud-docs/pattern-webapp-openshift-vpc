---
copyright:
  years: 2024
lastupdated: "2024-04-20"

subcollection: pattern-webapp-openshift-vpc
keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Service management design

**Management and Monitoring**

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
