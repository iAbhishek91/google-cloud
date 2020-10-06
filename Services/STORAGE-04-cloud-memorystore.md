# Cloud memory store

- In memory database offering from google.
- This is based on Redis protocol. Hence if your application is using Redis, can easily migrated to GCP. **Easy lift and shift**.
- Ideal for application cache that provides sub-millisecond data access.
- It sits in between frontend application and cloud store. So when an application request some data from cloud storage, it first checks cloud memorystore and then fetches.
- It improves the performance of the application by reducing the fetch time from database.
- **Storage** upto 300 GB and n/w throughput of 12 GB/Sec.
- **SLA of 99.9%** availability with **automatic failover**.
- Integrated with stackdriver for monitoring.
- Patching of the nodes Redis deployments are managed by google.
