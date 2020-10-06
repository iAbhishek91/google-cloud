# Big table

- Google cloud big table **is a NoSQL**, wide column database service for terabyte applications.
- As its NoSQL it has partially filled columns.
- Span up to 1000s of columns and billions of rows.
- capable of storing peta byte of data.
- very low latency.
- High throughput for both read and write
- fully managed by GCP.

- Big table are **useful** for database with single lookup keys. They also popularly used as a persistent hash tables.
- is popular for operational and analytical system like IoT, Financial analysis etc.
- act as a storage engine for MapReduced operations, stream processing and machine learning applications

- **accessed** using open source HBase API. *Native database for Apache hadoop, HBase is a open source project managed by Apache Hadoop*.
- Same API are useful in increasing portability.

- **Reason to choose Big Table** instead of Hadoop
  - Managed (upgrades and restarts transparently done by Google)
  - Scalable without down time.
  - Security: Like cloud-storage, cloud Bigtables contents are always encrypted at rest and in flight.
  - Authorization via IAM.
  - Great choice for analytical and operational application. Also for machine learning applications.

> NOTE: choose Big Table over cloud firestore if transactional consistency is NOT required.
> Cloud filestore scale down well, and Cloud bigtable scales up well.
> Cloud filestore is a document database, however big table is wide column database.

- Google big table is the same database used Google it self in Search, Maps and analytics and Gmail.

- **interaction between GCP services** and other third party clients.
  - Using *Application API* data can be read from and to cloud bigtables through data service layer like managed VMs. HBase rest server or Java server using HBase client. This data will be serve to application dashboard and data services.
  - *Streaming* data can be streamed in (event by event) through a variety of popular stream processing framework like cloud dataflow streaming, spark streaming and storm.
  - *Batch processing* read to and from big table using batch processes like hadoop map reduce, dataflow, or spark.

## What is NoSQL

- in brief, in traditional relational database each row of data have similar structure, which are enforced by the table that you define. However this strict rules are not required for all the application, and hence NoSQL type database was introduced. Hence all the rows may not have same columns.
