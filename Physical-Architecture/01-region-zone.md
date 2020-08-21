# Physical Architecture

Region are geographic areas consists of zones. At least 160 km difference between the zones.

Zones are deployment areas of GCP within a region.
Zones are single failure domain within a region.
However, Zone mostly consist of multiple data center or building.
To deploy application in HA mode, app need to be deployed on multiple zones.

Disaster recovery plan is a plan of recovering data and services in case or entire region failure (for example: due to natural resources).

## Type of resources

- **Zonal resources**: single zone (for example: VM instance)
- **Regional resources**: deployed with redundancies on a specific region. They are multi-zone resources and run with HA.
- **Multi-regional resources**: these service span over multiple region. optimized availability, performance & resources efficiency. There are trade-off as multi-region comes with latencies. This trade-off are mentioned on the product specific basis. (for example: app-engine, cloud-datastore, cloud-storage, google BigQuery)
