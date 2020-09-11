# Stack Driver

Stack Driver manages resources across different platform: AWS, GCP, On-Premise.

Stack driver are already integrated with many GCP services like: Compute engine, App Engine, BigQuery, Cloud Datastore, GKE, Cloud Pub/Sub, cloud SQL and many more.

Stack driver logs are stored for limited number of days. For admin activity logs are kept for 400 days, and data access audit logs are kept for only 30 days.

However we can export logs for analysis and store it in persistent storage if required.

Below are the components available under stack drivers.

## Monitoring

- In Kubernetes and GKE, monitoring application across multiple cloud provider.
- Check for uptime and health checks.
- Provides dashboard and alerts mechanism.

## Trace

- Used by DevOps team.
- use to get the latency, and other sample data per URL statistics.

## Debug

- Used by DevOps team
- Debug the application source code running on production with out logs.
- Debugger works best when source code is available on cloud-source-repository

## Logging

- Centralized logging service.
- Application logs, system logs, platform logs.
- able to process logs, search logs view, filter and export(in big query, cloud pub/sub, storage) just like splunk.

## Error reporting

- Extract errors, and groups them.
- notifies users about the errors.

## Profilers (BETA)

## Installing Stack driver agent with VM instances

[GCP Docs](https://cloud.google.com/monitoring/agent/installation?_ga=2.259618700.-709608325.1596613385&_gac=1.83054052.1596613385.CjwKCAjwsan5BRAOEiwALzomX4P0FSrVgDyfLlilFkWE5WIykwC79JXGYy8bzTet51qSl_pgH6_K5xoCtrYQAvD_BwE#agent-install-debian-ubuntu)

### Features

- Agent gathers system and application metrics from your VM instances and sends them to Monitoring.
- can be installed on compute engine and EC2 instances.

### Installation

- make sure, 250 Mb of main memory on the VM | supported OS version
- Download & execute the shell script for downloading and installing the agent.
- restart the service of the agent.
- may delete the script as its not required any more.

## Access the logs

- Validate the stack driver agent is up and running.
- validate the log folder in the VMs.

```sh
sudo service stackdriver-agent status
sudo grep collected /var/log/(syslog,message}) | tail
```

- Navigate to monitoring from cloud and go to the dashboard to verify the logs are getting generated.
