---

copyright:
  years: 2024
lastupdated: "2024-01-23"

subcollection: <repo-name>

keywords:

---

# Architecture decisions for service management
{: #service}

The following sections summarize the architecture decisions for service management for the web app multi-zone resiliency pattern.

## Architecture decisions for monitoring
{: #monitoring}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Operational monitoring of cloud infrastructure and services | Monitor system health to detect issues that might impact the availability of the system and application. | - IBM Cloud Monitoring \n - BYO Monitoring Tool | IBM Cloud Monitoring | IBM Cloud Monitoring collects and monitors operational metrics for cloud infrastructure as well as the cloud platform and services and provides a single view for all metrics |
| Operational monitoring of applications | Monitor app health to detect issues that might impact the availability of the app. | - IBM Cloud Monitoring \n - Instana (SaaS) \n - BYO Monitoring Tool | IBM Cloud Monitoring + Instana (SaaS) | Instana is used along with IBM Cloud Monitoring to get more application performance metrics and automate application performance management. Instana provides data and actionable insights to monitor the applications and automate root-cause analysis. |
{: caption="Table 1. Architecture decisions for monitoring" caption-side="bottom"}

## Architecture decisions for logging
{: #logging}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Log monitoring of cloud infrastructure and services | Monitor operational logs to detect issues that might impact the availability of the system and application. | - IBM Cloud Logging \n - BYO Logging Tool | IBM Cloud Logging | IBM Cloud Logging collects operational logs from applications, platform resources, and infrastructure and provides interfaces to view and analyze all logs. |
| Log monitoring of web app | Monitor application operational logs to detect issues that might impact the availability of the app.| - IBM Cloud Logging \n - Application Logging Tool \n - BYO Logging Tool | IBM Cloud Logging + Application Logging Tool | Use the Application Logging Tool to send application logs to IBM Cloud Logging and aggregate application-specific log details. |
| Log monitoring of DB | Monitor database logs to detect issues that might impact the availability of the database.| - IBM Cloud Logging \n - DB Tools \n - BYO Logging Tool | IBM Cloud Logging + Application Logging Tool | Use the DB tools along with IBM Cloud Logging to get more DB-specific log information. |
{: caption="Table 2. Architecture decisions for logging" caption-side="bottom"}

## Architecture decisions for auditing
{: #auditing}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Audit logging | Monitor audit logs to track changes to cloud resources and detect potential security problems. | IBM Cloud Activity Tracker \n - Hosted Event Search \n - Event Routing   | IBM Cloud Activity Tracker- Hosted Event Search | IBM Cloud Activity Tracker-Hosted Event Search provides interfaces to capture, store, view, search, and monitor user-initiated actions to provision, access, and manage IBM Cloud resources. |
{: caption="Table 3. Architecture decisions for auditing" caption-side="bottom"}

## Architecture decisions for alerting
{: #alerting}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Operational alerts | Provide a mechanism to identify and send notifications about operational issues that are found across application and infrastructure. | IBM Cloud Monitoring +  IBM Cloud Logging + Event Notifications | IBM Cloud Monitoring +  IBM Cloud Logging + Event Notifications | IBM Cloud Monitoring and IBM Cloud Logging support the configuration of alerts to detect operational issues and send notifications to targeted channels. \n Event Notifications are used to route the alert events to service destinations to automate response actions. |
| Audit alerts | Provide a mechanism to identify and send notifications about issues that are found in audit logs. | IBM Cloud Activity Tracker + IBM Monitoring +  Event Notifications | IBM Cloud Activity Tracker + IBM Monitoring +  Event Notifications | IBM Activity Tracker supports the configuration of alerts to detect audit issues and send notifications to targeted channels. \n Event Notifications are used to route the alert events to service destinations to automate response actions.                            |
{: caption="Table 4. Architecture decisions for alerting" caption-side="bottom"}

## Architecture decisions for event management
{: #event management}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Event management | text | text | text | text| text|
{: caption="Table 4. Architecture decisions for event management" caption-side="bottom"}

## Architecture decisions for automated deployment
{: #automated deployment}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Automated deployment | text | text | text | text| text|
{: caption="Table 5. Architecture decisions for automated deployment" caption-side="bottom"}

## Architecture decisions for management/orchestration
{: #management/orchestration}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Management/Orchestration | text | text | text| text|
{: caption="Table 5. Architecture decisions for management/Orchestration" caption-side="bottom"}
