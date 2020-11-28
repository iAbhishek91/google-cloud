# Data Analytics with Big Data

Data analytics includes **ingestion**, **collection**, **processing**, **analyzing** and **visualizing** of data.

Below are the fully managed services provided by GCP which are scalable. (they are called as serverless services are Google man the infra.)

## Cloud DataProc

- Cloud dataproc runs on compute engine.
- managed Apache Hadoop and Apache spark/pig/hive service. *User have to request for the hadoop cluster in 90 seconds or less run their instance in dataproc. User also need to input the number and type of the compute engine VMs you control.*
- User need to pay for the life of the hadoop cluster you create. The cost is per seconds, subject to § minute minimum billing. Note: compute engine cost is not the only cost involved with dataproc. There can be several other.
- Easily migrate to on-premise hadoop jobs to cloud.
- generally takes 90 seconds to start a cluster.
- integrated with cloud dataflow and big query. Common flow, data enters GCP from pub/sub, pre-processed in dataflow and then transferred to dataproc for processing using map/reduced function. Once the data is processed the data is saved in Bg=ig Query or cloud storage.

- **Usecase**
  - great when we have data set of known size.
  - or when you want to manage of the cluster size yourself. (Not ideal for real time data, or unpredictable array of data)

- map/reduce function. Map and reduce are two different function which completes the entire process

## Big Query (analyzing historical data)

- managed analytics.
- one of the oldest analyzing service that was added in GCP.
- its a kind of database.
- its a **serverless, scalable data warehousing services**.
- supports petabytes of data sets.
- in built with in-memory BI engine and ML
- Supports standard ANSI:2011 SQL dialect for querying. Hence use need not learn different language(DSL) to use Big query.
- input data sets can be taken from cloud storage, Bigtable, spreadsheets(from google drive).
- Automatically replicate data to keep a seven day history of changes.
- Integrates with 3rd party tools like Informatica and Talend.
- for playing, it comes with lots of public data sets. One can use that to play around the platform.

## cloud DataFlow (processing data in bach or real-time)

- process data from stream(real time) from pub/sub or in batch from cloud storage.
- processing service based on apache beam. *Google is one of the key contributor to Apache beam open source project*.
- cluster size is automatically dynamically decided for you depending on the data.
- separate instance provisioning required.
- user creates data pipeline for both batch and streaming data.
- it generally take input form big query database process it using map or reduced function and write it to cloud storage. Each step can be scaled independently.
- its used for pre-processing of data as it enters cloud
- tightly integrated with cloud Pub/Sub, BiqQuery, cloud Machine learning.
- charged only for the time the job is executed.
- seamlessly **transit between batch and streming data**
- can convert **apache beam job to apache spark**

- **Usage**
  - it deals with real time data. The size of the data is manged by google.
  - it is a general purpose ETL tool.
  - can used in fraud detection of streaming data.
  - connector for kafka makes it easy to integrate with Apache kafka stream.

> It is very similar to dataproc. Do refer to the "BIGDATA-02-dataproc-or-dataflow.png"

- **Pipeline for bounded source in dataflow**
  - cloud storage:
    - data are saved in buckets
  - cloud dataflow:
    - read from cloud storage
    - modify the data(filter, do specific analysis)
    - write to durable storage
  - cloud storage/bq
    - in the sharded data.

- **Pipeline for unbounded source in dataflow**
  - cloud pub/sub:
    - stream of data coming to dataflow.
  - cloud dataflow: (pipeline in dataflow can be complex) *we can introduce data processing concepts like watermark windowing, count*
    - read from cloud storage
    - modify the data(filter, do specific analysis)
    - write to durable storage
  - cloud storage/bq/bigtable/etc
    - in the sharded data.

## Cloud DataPrep

Data analysis tool, which is used for cleaning, exploring and preparing data for analysis and machine learning.
Integrated partner service operated by **Trifacta**

## Cloud DataLab (analyzing and visualizing data)

- Interactive tool for data **exploration**, **analysis**, **visualization** and **machine learning**.
- Runs on compute engine. (but that is automated on GCP with appropriate tools like Jupyter, we need not create a VM prior)
- and may connect to multiple cloud services.
- Its built on open source Jupyter Notebooks platform. This is a standard for visualizing and analyzing data sets.
- Can perform data analysis on BigQuery, Cloud ML Engine and cloud storage.
- It supports Python, SQL and JS.

## Cloud Pub/sub (ingestion of data at scale)

- managed message queue service.
- based on publish/subscription pattern.
- pub/sub act as an entry point to GCP-based analytics services.
- Share data between application in async manner.
- integrated with services such as cloud storage(for archival) and cloud data flow(for analytics). Pub/Sub pushes the data to this services.
- synchronous cross-zone message replication.
- e2e encryption, IAM and Audit logging.
- store data for 7 days, if the data is not consumed.

> NOTE: Pub/Sub is not a durable data store, but can store data in staging location for temp until it goes for processing in data proc or data flow.
