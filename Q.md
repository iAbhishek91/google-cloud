# Questions

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

| ad | cloud-datastore|cloud-bigtable| cloud-storage | cloud-SQL | cloud-spanner |cloud-bigquery|
|---|---|---|---|---|---|---|
| Type | NoSQL Document | NoSQL Wide Column | blobstore | RDBMS for OLTP | RDBMS for OLTP | RDBMS for OLAP |
| Transactions | Yes| single row | No | Yes | Yes | No |
| Complex queries | No | No | No | Yes | Yes | Yes |
| Capacity | TB+ | PB+ | PB+ | TB | PB | PB+ |
Unit size | 1 MB/entity | ~ 1- Mb/cell, ~ 100Mb/row | 5 TB/obj | Determined by DB engine | 10240 Mib/row | 10 MB/row |
| Best for | semi structured app data, durable key-value data | "Flat" data, heavy read/write, events, analytical data | structured and unstructured binary or object data | Web frameworks, existing applications | large scale db app (> ~ 2 TB) | Interactive querying, offline analytics |
|Use cases | Getting started, app engine app | AdTech, Finantial & IoT data | Images, large media, backups | User credentials, customer orders | whenever high i/O, global constency in needed | Data warehousing |