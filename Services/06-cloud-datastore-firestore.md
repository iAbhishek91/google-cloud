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
- its lets you perform SL like queries.
- free daily quotas: few small operations(storage, reads, writes and deletes) can be performed without any charge.

- **use cases**: store data structure data from app engine apps.
  - designed for application backends.
  - build soln which spans app engine and compute engine and cloud-datastore is the integration point.
  
## Firestore

- Its next gen db or upgraded version of Datastore.
