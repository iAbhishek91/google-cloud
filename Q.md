# Questions

## launching URL of google cloud

`https://cloud.google.com`

## what is the primary customer benefit of measured service

Measured service is one of the main paradigm of cloud computing, where customer can provision, use and pay for the amount of resources consumed. every thing on demand.

## what is relation between Project and Region

## Where we can find the events triggered by some service by user or by GCP

- "Activity list" tab of the GCP console.
- The specify the action in detail, what action, by whom and when

## Where we can find any GCP recommendation based on our cloud use

Under cloud console, under recommendation tab.

## what level in GCP resource hierarchy is billing setup

at project level

## Explain in details gcloud & gsutil command

- refer 03a-gcloud.md and 03b-gsutil.md

## Services and API are enabled on a per-____ basis

- **Project**, folder, organization, billing account

## How to choose the size of the VMs

Based on the processing powers are required only when we require huge computing power.

However using small VMs are better when we use have option to split the processing power.

## What are extended memory

## What are default processor based on zone

sanibridge processor for us-central-1? study more about these processor.

## Mention few scenario where you need to stop your VM

- upgrade or add more CPU or memory
- remove or set a new static IP
- modify instance tag.

## Mention few properties that can be changed when a VM is running

- labels
- Internal & External IP type
- Allow or disallow HTTP /HTTPS
- Boot disk - What to do after the VM terminates
- Availability policies

## Mention few permanent properties of VM which cant never be changed

- name
- Region and Zone
- Image

## There are multiple storage options for a VM (mentioned in Persistent-disk.md), which option to choose when

In most of the scenario the common option recommended by google is to add a persistent disk to your VM.

for critical data, choose **Regional Block storage** else **Zonal block storage** for redundancy.

for high performance additionally we can choose **local storage**.

for better performance of the choose SSD over HDD

if application is not concerned with latency, cloud-storage is best option.

## What are the options to connect cloud storage

either using API posting data using SDK or we can  use *cloud storage Fuse* tool to mount a cloud storage bucket to your compute engine instance.

> NOTE: Cloud storage is a object storage but like a block storage in this case.

## List the event on which Local SSD data will be persisted

- reboot of guest OS
- host goes through maintenance event, and live migration is configured
- if host system experience a host error, compute engine makes a best effort to reconnect to the VM and preserve local SSD (Note this do NOT come with 100% guarantee)

## list the event on which Local SSD data will not b persisted

- manual stop of VM
- shutdown of OS with force stopping the VMs
- preemptible VM going through preemption process
- if "stop on host maintenance events" is configured, and instance goes though a host maintenance event.
- if host system experience a host error, and do not recover with 1 hour, compute engine  does not attempt to preserver the data on your local SSD.
- misconfiguration of local SSD so that it becomes unreachable.
- disable project billing. the instance will stop and data will be lost.

## Where do local SSD physically located

On the same server(hardware) where the VMs is hosted. Hence they can be created only when instance is created and cannot be used as boot device. Before use we need to format and mount the disk.

## How many number of local SSD can be configured

It depends on machine type you can attach 1 - 8, 16 or 24 max local SSD to single VM. *For example: all N1 machine type allow 1-8,16 or 24 | N2 machine type with 2 to 10 vCPU allow 1,2,4 or 8 | N2 machine type with 42 to 80 vCPU allow 8*

## How to persist data from local block storage on some other media

Manually we one need to perform that task.

## What are the constraints of taking snapshot of a VM which have local SSD

The problem happens when snapshot is taken on a VM which has /etc/fstab configured with local SSD and try to mount in a another VM.

As remedy we have to remove the entry of local SSD from the fstab before loading the snapshot on another VM.

## Local SSD performance is better than Persistent storage, but is there any other factors to improve the performance

Yes, local SSD connects with VM using SCSI or NVMe interfaces. The interface driver should be available in the OS image we are using to create the VM. NVMe is faster than SCSI (max IOPS R/W of NVMe 2,400,000/1,200,000, R/W of SCSI is 900,000/800,000)

To get max performance, attach multiple local devices(16 to 24), group them using logical volume. Consider using VM with 32 or more vCPU.

## What are the ways we can mitigate VMs unavailability

- **Regional MIG**: distributes your VMs across multiple zone.
- **Auto Healing**: to recreate a failed VM. (For auto-healing, VM state is not sufficient, you may want to recreate th eVM is application fails, crashes or run out of memory)
- **Load Balancing** to direct user not the healthy VMs.

> Note: Autoscaling is not a good option in case of failure.

## What is the correct size of regional MIG

Google recommends to over-provision your VM based on the application needs, so that in case of failure of a zone, the entire group should not fail. or more than expected VMs are not available.

## How to update image template, what are the limitation

INCOMPLETE
https://cloud.google.com/compute/docs/instance-groups/autohealing-instances-in-migs#autohealing_behavior

## what are frequency of compute engine's VM

There are two type of maintenance type:

- **host maintenance**: kernel and hardware upgrade. Once every two week. Live migration is required.

- **lightweight**: hypervisor or network stack upgrade. 1-2 times per week. Live migration is not required.

## What factor determine auto-upgrade in GKE

If any of the "Release channel" is selected as master version.

## When to choose which release channel in GKE

- rapid: for non-prod cluster, experiment of new features etc.
- regular: for prod cluster, gives a balance option between stability and new feature
- stable: for prod cluster, where maturity is more important than new features.

## How do you avoid GKE version auto upgrade disruption

- option-1
  - create a pre-prod cluster and choose **rapid** as the channel.
  - This will give you 2-3 months of time to test the new feature if its release to **regular** channel.
  - If 2-3 months are not sufficient, choose **maintenance exclusion**.
- option-2
  - manually upgraded to new version. (more control of time of upgrade, and better predictability)

## Characteristics of maintenance exclusion

- mainly used to postpone auto-upgrade of K8s version.
- select three
- cant be recurrence
- can be configured for new or existing cluster.

## Compare all the storage options provided by GCP

| # | cloud-datastore|cloud-bigtable| cloud-storage | cloud-SQL | cloud-spanner |cloud-bigquery|
|---|---|---|---|---|---|---|
| Type | NoSQL Document | NoSQL Wide Column | blobstore | RDBMS for OLTP | RDBMS for OLTP | RDBMS for OLAP |
| Transactions | Yes| single row | No | Yes | Yes | No |
| Complex queries | No | No | No | Yes | Yes | Yes |
| Capacity | TB+ | PB+ | PB+ | TB | PB | PB+ |
Unit size | 1 MB/entity | ~ 1- Mb/cell, ~ 100Mb/row | 5 TB/obj | Determined by DB engine | 10240 Mib/row | 10 MB/row |
| Best for | semi structured app data, durable key-value data | "Flat" data, heavy read/write, events, analytical data | structured and unstructured binary or object data | Web frameworks, existing applications | large scale db app (> ~ 2 TB) | Interactive querying, offline analytics |
|Use cases | Getting started, app engine app | AdTech, Finantial & IoT data | Images, large media, backups | User credentials, customer orders | whenever high i/O, global constency in needed | Data warehousing |

## Compare Standard and Flexible App engine

| # | Standard | Flexible |
|---|---|---|
| *Instance startup* | Milliseconds | Minutes |
| *SSH access* | No | Yes (not by default) |
| *Write to local disk* | No | Yes (but ephemeral) |
| *Support third party binaries* | No | Yes |
| *N/W access* | via App engine service | Yes |
| *Pricing model* | After free daily use, pay per instance class, wioth automatic shutdown | Pay for resource allocation per hour, no automatic shutdown |

## Compare different network services with feature and use cases

| Services | key features | Use Case |
|---|---|---|
| HTTP(s) Load balancing | Global load balancing of HTTP(s) endpoints | CMS deployed in multiple regions |
| TCP Load Balancing | Regional load balancing of TCP/UDP endpoints | Distribute traffic evenly across gaming backend service |
| VPC | Private network within GCP | Deployed GCE VMs that are not exposed to the public internet |
| Cloud Interconnect | Dedicated network to extend local data center | Access cloud resoruces from local application with low latency |
| Cloud VPN | Secure access to GCP resrouces through public internet | Cheaper option to extent local data center to cloud |
| Peering | Directly access cloud resources with reduce egress fee | Secure access to GCP and G suite resoruces via direct or carrier peering |

## What are difference between GKE and App engine

| # |K8s engine | App Engine Flexible | App Engine Standard |
|---|---|---|---|
| *Language support* | Any | Any | Java, Python, Go, PHP |
| *Service model* | Hybrid | PasS | PaaS |
| *Primary use case* | Container-based workloads | web and mobile app, container-based workloads | web and mobile applications |

## do GCP uses same network as Google

GCP provides two service tiers for traffic optimization: **standard**, **premium**.

Two type Standard and Premium services tiers provides trade off between performance and cost.

Premium is similar to Google's premier network backbone, however standard regular connectivity based on ISP based networks.

However premium is default.

[Ref](https://cloud.google.com/network-tiers/docs/overview)

## one benefit of applying firewall rules by tag rather than by address

When a VM is created with a matching tag, the firewall rules apply irrespective of the IP address it is assigned.

## How to create multiple compute engine with same config

1. Create an instance template
2. Create an instance group

## How to make sure that load balancer always route traffic to healthy VMs

- Configure health check for each VMs that are pointed by load balancers.
- When configuring the load balancer backend section select the health check that was created on previous step.
- validate the healthy nodes once the load balancer starts under healthy column. Thats it.
