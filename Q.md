# Questions

## launching URL of google cloud

`https://cloud.google.com`

## Where we can find the events triggered by some service

- "Activity list" tab of the GCP console.

## Explain in details gcloud & gsutil command

- refer 03a-gcloud.md and 03b-gsutil.md

## Services and API are enabled on a per-____ basis

- **Project**, folder, organization, billing account

## How to choose the size of the VMs

Based on the processing powers are required only when we require huge computing power.

However using small VMs are better when we use have option to split the processing power.

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

## How to create multiple compute engine with same config

1. Create an instance template
2. Create an instance group

## How to make sure that load balancer always route traffic to healthy VMs

- Configure health check for each VMs that are pointed by load balancers.
- When configuring the load balancer backend section select the health check that was created on previous step.
- validate the healthy nodes once the load balancer starts under healthy column. Thats it.
