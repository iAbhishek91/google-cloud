# Cloud SQL

- Its a Storage service provided by GCP.
- We can create managed **PostgreSQL** and **SQL database** instance.
- Fully managed service.
- capable of handling terabytes of storage. 30 TB with 40000 IOPS and 416GB of RAM 64 vCPU.
- Auto fail overs.
- Read replicas, streaming replicas across the zones.
- Backup on-demand or on schedule.
- Scaling vertically(by changing the machine type) or horizontally(read replicas) is possible.

- Users can run own instance of database services on compute-engine(many user does that), however its better to use managed services.

- **Google security**: firewalls, encryptions when stored in backups, tables.
- Also cloud SQL instance may be launched within VPC for additional security.

- **integration with other GCP services**:
  - integrated with *App engine* using standard drivers.
  - also *compute engine* instances can be authorized to access cloud SQL instances using an external IP address. They need to be in same Zone.
  - *other external services* application or clients can connect with Cloud SQL using MySQL drivers (for example toad, sql workbench). Also external read replicas can be configured.

- **Replica service**
  - this creates replicas on different zones.
  - replicas is for resiliency.
  - streaming replica are used to achieve automatic failover replicas.

- **Backup recovery**
  - automated or on-demand backups
  - also come with point in time backups.

- **Import/Export**
  - mysql dump or mysql csv files.

- **Scaling**
  - scale up: needs machine restart as the machine capacity will be increased.
  - scale out: using read replicas.
  - its recommended to use cloud spanner if horizontal scaling is requirement. *discussed further on cloud-spanner.md*

- **Choosing connection type** : determine how *secure*, *performance* and *automated* it will be.
  - If *you are in the same project, and co-located in same region* : for maximum performance and security: select private connectivity using private IP address. It will not expose data to internet.
  - If *you are in another project or region or trying to access outside GCP*: recommended is cloud proxy, authentication, encryption an key rotation for me or authorize network where specific IP address will be allowed to connect to the database instance.

> REFER the 2a connectivity type.
> REFER the decision tree on RDBMS option google provide.


Shared-core machines are good for prototyping, and are not covered by Cloud SLA.
Each vCPU is subject to a 250 MB/s network throughput cap for peak performance. Each additional core increases the network cap, up to a theoretical maximum of 2000 MB/s.
For performance-sensitive workloads such as online transaction processing (OLTP), a general guideline is to ensure that your instance has enough memory to contain the entire working set and accommodate the number of active connections.

Storage type

SSD (solid-state drive) is the best choice for most use cases. HDD (hard-disk drive) offers lower performance, but storage costs are significantly reduced, so HDD may be preferable for storing data that is infrequently accessed and does not require very low latency.
There is a direct relationship between the storage capacity and its throughput.
