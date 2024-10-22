---
copyright:
  years: 2024
lastupdated: "2024-04-29"

subcollection: pattern-webapp-openshift-vpc
keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Management and monitoring

{: #management-monitoring}

The recommended approach for multi-cluster management and monitoring is to use IBM Cloud tools that include IBM Log Analysis and IBM Cloud Monitoring. This approach enables application cluster metrics log aggregation and central management within IBM Cloud.

## IBM Log Analysis

{: #log-analysis}

You can use IBM Log Analysis to add log management capabilities to Red Hat OpenShift VPC clusters and provide for the following:

- Customizable user interface for live streaming of log tailing, real-time troubleshooting issue alerts, and log archiving.
- Quick integration with the cluster via a script.
- Aggregated logs across clusters and cloud providers.
- Historical access to logs.
- Highly available, scalable, and compliant with industry security standards.
- Integrated with IBM Cloud IAM for user access management.

## IBM Cloud Monitoring

{: #ibm-cloud-monitoring}

You can use IBM Cloud Monitoring to monitor the performance and overall system health of Red Hat OpenShift VPC clusters and provide for the following:

- Customizable user interface for a unified view of cluster metrics, container security, resource usage, alerts, and custom events.
- Quick integration with the cluster via a script.
- Aggregated metrics and container monitoring across clusters and cloud providers.
- Historical access to metrics that is based on the timeline and plan, and the ability to capture and download trace files.
- Highly available, scalable, and compliant with industry security standards.
- Integrated with IBM Cloud IAM for user access management.

For more information, see [how to forward application and cluster metric data to IBM Cloud Monitoring](/docs/openshift?topic=openshift-health-monitor\#openshift_monitoring)

## Flow Logs for VPC clusters

{: #flow-logs}

Configure IBM Cloud Flow Logs for VPC to gather information about the traffic entering or leaving VPC cluster worker nodes. Flow logs are stored in an IBM Cloud Object Storage instance and can be used for troubleshooting purposes, adhering to compliance regulations. For more information, see [Flow logs use cases](/docs/vpc?topic=vpc-flow-logs&interface=ui#flow-logs-use-cases).

Using IBM Cloud Monitoring can create alerts when workloads need more resources.
{: note}

## Resource Management

{: #resource-management}

Set up spending notifications from the IBM Cloud billing console. You can set quotas or resource limits on clusters and namespaces. The cluster administrators can make sure that teams that share a cluster don't consume more than their fair share of compute resources, memory and CPU, by creating a [Resource Quota object](https://kubernetes.io/docs/concepts/policy/resource-quotas/) for each Kubernetes namespace in the cluster. If the cluster admin sets a compute resource quota, then each container within the deployment template must specify resource requests and limits for memory and CPU, otherwise the pod creation fails.
