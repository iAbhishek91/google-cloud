# Stack Driver

Stack Driver manages resources across different platform: AWS, GCP, On-Premise.

Stack driver are already deeply integrated with many GCP services like: Compute engine, App Engine, BigQuery, Cloud Datastore, GKE, Cloud Pub/Sub, cloud SQL and many more. StackDriver also integrate with other partner services like splunk, netskope, pagerduty etc.

Below are the components available under stack drivers.

## Monitoring

- Check for uptime and health checks.
- Provides custom dashboard and alerts mechanism.

### Disable or enable Monitoring for a project

From APIs & services, enable/disable **Cloud Monitoring API**.

### what is Workspace

>GOLDEN RULE: - A **project can be associated only with one workspace**. But **one workspace may contain multi-project**.

- Workspace is the root entity that holds monitoring and configuring information of a project.
- Name of the workspace *CANT be changed* is created based on a GCP project, and this is known as the **host project**.
- The monitoring workspace is deleted automatically with the **host project**.
- To remove **host project** from the workspace, we need to merge. After merge GCP project do not be a host project anymore and we can then remove it. *Project owner role is required for this operation*.
- We can add *multiple (100) GCP project & AWS accounts* as part of one workspace. **Multi-project** workspace are created when we have requirement of isolating projects monitoring. *As authorized user to a workspace will have access to all the project included in that workspace.*.

> Best practice: If we want multi-projects workspace, its recommended to create a new project as a host project, and create a workspace. Which inturn monitor all the actual projects and AWS accounts.

- **Creating a workspace**: for new project for which workspace is not there, go to monitoring and workspace is automatically created or added to a existing workspace depending on the multi-project workspace created previously.
  - if the project is already associated with a workspace, we can't create.
- **Two way to create multi-project workspace**: *ADD* and *MERGE* (once workspace is merged it cant be reverted.)
- **Authorization** user needs access to GCP host project to get access to the workspace.
- **Delete a project**: cant delete a workspace only, need to delete the host project.

> NOTE: workspace are always created from cloud console only.

### Dashboard

Dashboard help you to create custom dashboard that holds charts of the metrics. Can visualize it as grafana.

### Alerts

- Can visualize alerts when something goes wrong.
- There are **three part** to configure a alert:
  - **condition**: threshold, resource parameter, many more
  - **Whom to notify**: Select notification channels. Define notification channel in the alert section.
  - **Define the steps to mitigate the issue**: This doc will be sent over email to everyone.

> Best Practices: Alerts are recommended to be created on symptoms and not necessarily on causes.
> Secondly, use multiple notification channel for notification (to avoid single point of failure). Lastly, set alerts actionable, not for everything.

### Uptime checks

Checks the availability of the public services. It can be of type HTTP, HTTPs or TCP.

It can app engine app, or compute engine or load balancer or AWS host or any APP url.

We can create alerting policy based on the uptime check.

### Resource groups

Resource groups enable you to create groups based on *resource type*, *project*, *security group*, *region* or *name*.

### How to connect with AWS

There should be a GCP project to hold the AWS connector.

### Price

Monitoring charges for the volume of ingested metric data that exceeds the free monthly metric allotment and for Cloud Monitoring API read calls that exceed the free monthly API allotment. Non-chargeable metrics and Cloud Monitoring API write calls don't count towards an allotment limit.

**NON CHARGEABLE metrics** are: Google cloud metric, Anthos metric, Istio metric, Knative metric, GKE metric.

**CHARGEABLE metrics** are: AWS metric, Custom metric, External metric, Logs based metric

There is NO CHARGE for creating workspace.

Alerts can be created on cloud monitoring cost.

## Trace

- Used by DevOps team.
- use to get the latency, and other sample data per URL statistics.
- Its available for App engine, Google HTTP load balancer.
- Application instrumented with the stack driver trace.

## Debugger

- Allow to debug the state of the running application in realtime, without stopping or slowing down significantly.
- Used by DevOps team, can take snapshot of the running state of the application. Also can inject a new logging statement in the application.
- Debug the application source code running on production with out logs.
- Debugger works best when source code is available on cloud-source-repository
- It also supports multiple languages: Java, Python, NodeJS, and Ruby.

## Logging

- Centralized logging service.
- Application logs, system logs, platform logs.
- able to process logs, search logs view, filter and export(in big query, cloud pub/sub, storage) just like splunk.
- Stack driver logs are stored for limited number of days. For admin activity logs are kept for 400 days, and data access audit logs are kept for only 30 days.
- However we can export logs for analysis and store it in persistent storage if required.

### Where logs are stored

Logs are stored in bucket. By default *two bucket is automatically created* per project **_Default**(30 days) and **_Required**(400 days). For custom retention period one can create their own storage.

> NOTE: retention is nothing but lifecycle policies on cloud storage.

### Other ways of exporting logs

Apart from cloud logs, we can use logs sink which includes channels to route traffic to other source.

Logs can be exported to BigQuery(for querying large set of data using SQL - for example: by analyzing network logs it can be to reduce cost by analyzing where most of the traffic are coming from, analyse network for incident and usage), cloud storage(for storing data) or to data studio(to play with the logs data).

### Logging agent

Like stackdriver monitoring agent there are logging agent available, we can install that in all the VM instances for compute engine and EC2 engines.

### Excluded logs

- We can exclude logs as per requirement from log router. *exclusion is part of sink under log router*.
- FREE logs cant be excluded or disabled.
- We can create 50 exclusion rules *can be based on filter or resource type*.
- Excluded logs aren't visible for log viewer, even they are not available for *Error reporting* and *Cloud Debugger*.
- There are two kind of exclusion:
  - *exclusion based on filters*
  - *exclusion based on resource type*

### Pricing

Based on the ingested log data that exceeds the free monthly log allotments. Few logs are FREE *cloud audit logs, access transparency logs* and are never charged or added up in the log allotment limit.

One can create a alert on monthly log bytes ingested.

## Error reporting

- Extract errors, and groups them.
- notifies users about the errors.
- as of now its available for APP engine, compute engine and EC2.
- It support almost all major languages. Java, Go, NodeJS, Python, Perl etc.

## Profilers (BETA)

## Installing Stack driver agent with VM instances

> Note: Stack driver monitoring agent can be used with compute engine as well as with EC2 engine.

[GCP Docs](https://cloud.google.com/monitoring/agent/installation?_ga=2.259618700.-709608325.1596613385&_gac=1.83054052.1596613385.CjwKCAjwsan5BRAOEiwALzomX4P0FSrVgDyfLlilFkWE5WIykwC79JXGYy8bzTet51qSl_pgH6_K5xoCtrYQAvD_BwE#agent-install-debian-ubuntu)

> We can also define custom agent and feed it into stackDriver.

### Features

- Agent gathers system and application metrics from your VM instances and sends them to Monitoring.
- can be installed on compute engine and EC2 instances.

### Installation

- make sure, 250 Mb of main memory on the VM | supported OS version
- Download & execute the shell script for downloading and installing the agent.
- restart the service of the agent.
- may delete the script as its not required any more.

### Access the logs

- Validate the stack driver agent is up and running.
- validate the log folder in the VMs.

```sh
sudo service stackdriver-agent status
sudo grep collected /var/log/(syslog,message}) | tail
```

- Navigate to monitoring from cloud and go to the dashboard to verify the logs are getting generated.
