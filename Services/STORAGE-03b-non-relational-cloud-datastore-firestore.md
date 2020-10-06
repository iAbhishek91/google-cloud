# Datastore and Firestore

- This is another choice for **NoSQL** database after cloud-bigtable.
- Both are no SQL database and keeps semi-structured data.

## Datastore

- Datastore can horizontally scalable.
- fully managed
- automatic sharding and replication
- highly available
- highly durable
- *Unlike cloud-bigtable*: cloud-datastore supports transactions which impact multiple rows.
- its lets you perform SQL like queries.
- free daily quotas: few small operations(storage, reads, writes and deletes) can be performed without any charge.

- **use cases**: store data structure data from app engine apps.
  - designed for application backends.
  - build soln which spans app engine and compute engine and cloud-datastore is the integration point.
  
## Firestore

- Its next gen db or upgraded version of Datastore. Fire store can run in datastore mode(suitable for server projects) and Native mode.
  - When to use what?: if application is server project use datastore mode, for mobile and IoT use the native mode.
- Its no-sql document database.
- simplify storage, sync and offline support.
- like Cloud SQL and spanner, Firestore also support ACID transactions.
- Multi-region replication.
- Powerful query engine. hence we can run complex queries on the instance without any degradation.

- **Use case**
  - If requirement is Highly scalable nosql database.
  - suitable for Mobile, web IoT apps at global scale.
