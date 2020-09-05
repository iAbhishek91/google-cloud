# Anthos

- Anthos is a hybrid and a multi-cloud solution and service management.
- Anthos framework rests on k8s and GKE deployed on-premise.
- Anthos manages k8s and GKE on-premise create the foundation and manages using single controlplane.
- on-premise and cloud env stay in sync.
- rich set of tools is provided
  - Managing services on-premise and in the cloud.
  - Monitoring systems and services.
  - Migrating application from on premise VMs into your cluster.
  - Maintianing consistent polices across all clusters, whether on-premise or in the cloud.
- both GKE on premise and on cloud can access to GCP market place. this makes it easy to have same configuration across both the cluster.

- connection between the clusters
  - cloud interconnect is used to connect both the cluster on-premise and on cloud.
  - Anthos service mesh layer connects with cloud interconnect and with istio open service.
  - stacdriver is used for logging and monitoring of both GKE on-premise and cloud k8s clusters.
  - Anthos configuration management define the configuration of both the cluster using cloud interconnect. They remain in sync and empowers the cluster on both tht side. These policies are kept version controlled in *policy repository* (a git repository). This git repo can be placed anywhere in cloud or on-premise. The configurations are enforced by anthos agent on both the cluster.

Since both the cluster on different cloud env or on-premise are connected, single change in the repo will impact all the cluster and can be centrally managed.

## Resources

[Anthos General Overview:](https://cloud.google.com/anthos/)
[Anthos Technical Documentation](https://cloud.google.com/anthos/docs)
