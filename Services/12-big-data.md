# Big Data

Below are the fully managed services provided by GCP which are scalable. (they are called as serverless services are Google manges the infra.)

## Cloud DataProc

- Cloud dataproc runs on compute engine.
- managed Apache Hadoop and Apache spark/pig/hive service. User have to request for the hadoop cluster in 90 seconds or less run their instance in dataproc. User also need to input the number and type of the compute engine VMs you control.
- User need to pay for the life of the hadoop cluster you create. The cost is per seconds, subject to § minute minimum billing. Note: compute engine cost is not the only cost involved with dataproc. There can be several other.
- Easily migrate to on-premise hadoop jobs to cloud.

- **Usecase**
  - great when we have data set of known size.
  - or when you want to manage of the cluster size yourself. (Not ideal for real time data, or unpredictable array of data)

- map/reduce function. Map and reduce are two different function which completes the entire process

## Big Query

- managed analytics.
- its a kind of database.
- its data warehousing services.

## cloud DataFlow

- managed data stream and batch processing service based on apache bean.
- cluster size is automatically dynamically decided for you depending on the data.
- separate instance provisioning required.
- user creates data pipeline for both batch and streaming data.
- it generally take input form big query database process it using map or reduced function and write it to cloud storage. Each step can be scaled independently.

- **Usage**
  - it deals with real time data. The size of the data is manged by google.
  - it is a general purpose ETL tool.
  - can used in fraud detection of streaming data.

## Cloud DataLab

## Cloud Pub/sub

- managed message queue service.
- Share data between application in async manner.
