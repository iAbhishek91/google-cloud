# Cloud SQL

- Its a Storage service provided by GCP.
- We can create managed **PostgreSQL** and **SQL database**instance.
- Fully managed service.
- capable of handling terabytes of storage.
- Auto fail overs.
- Read replicas, streaming replicas across the zones.
- Backup on-demand or on schedule.
- Scaling vertically(by changing the machine type) or horizontally(read replicas) is possible.

- Users can run own instance of database services on cloud-engine(many user does that), however its better to use managed services.

- **Google security**: firewalls, encryptions when stored in backups, tables.

- **integration with other GCP services**:
  - integrated with *App engine* using standard drivers.
  - also *compute engine* instances can be authorized to access cloud SQL instances using an external IP address. They need to be in same Zone.
  - *other external services* application or clients can connect with Cloud SQL using MySQL drivers (for example toad, sql workbench). Also external read replicas can be configured.
