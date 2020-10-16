# Cloud spanner

Unique offering from GCP, this service is very similar to cloud-SQL.

- its a horizontally scalable RDBMS across regions and continents.
- NoSQL database scales very easily, Cloud spanner provide the same feature with RDBMS. Hence it brings best of SQL and NoSQL database.
- it allows transaction consistency at global scale.
- Synchronous and automatic replicas synchronously for high availability across globe.
- peta bytes of capacity.
- Support ACID(Atomicity, Consistency, Isolation and Durability) transaction.

- Cloud spanner instances run in one of the three region types:
  - Read Write
  - Read only
  - Witness

- **Use cases**: sharding your databases for high throughput.
  - or to maintain out grown single RDBMS instance
  - strong transactional consistency and DB consolidation
  - Global data with strong consistency.
  - common use cases: financial applications and inventory applications.

## Architecture of spanner

- It automatically replicate data in "n - cloud zone" can be on same or multiple regions.
- The data will be sync using google fiber network.
