# Google Kubernetes engine (Hybrid)

- These is Google's managed kubernetes cluster.
- production ready with HA and comes with SLA.
- GKE cluster can be customized
  - type of nodes (type of operating system and resource power)
  - network settings.
  - location type : zonal and regional (can manage for both master and worker nodes)
  - version of kubernetes
- Node (worker nodes) are google compute engines. Once the cluster are created you can view the VMs under compute engine. These same VMs can also be viewed form K8s console.
- "k expose deployment my-deploy --port=80 --type=LoadBalancer" creates a network load balancer with a public IP address. Hence app in the k8s cluster can be accessed using the public IP.
- "k autoscale my-deploy --max=5 --min=2 --cpu=80" auto scale deployment easily.
- also comes with **auto node repair**, **auto scaling**, **auto upgrade**.

> NOTE: Control plane are managed by Google, hence if we say we need 2 node cluster, both the node will be worker nodes. This is a reason its a managed K8s cluster.

## API thats need to be enabled for GKE

Google Kubernetes Engine API
and Google Artifact registry API

## Attribute for pricing

- Total number of nodes
- \# of zonal cluster: one is free
- \# of regional cluster
- Machine type: Regular or Preemptible
- Machine family: General purpose, compute-optimized, memory-optimized
- Series: N1, E2..
- Machine Type: n1-standard-16
- Local SSD
- Location(region)
- avg hours /day
- avg days/week
- persistent disk details

> Note: Anthos GKE clusters are exempted from GKE cluster management fee.

You will be charged for the VMs, and cluster management fee.

## node pool

- Node pool is group of nodes, that have same configuration.(they are like manged instance group in compute engine)
- Node pool uses "NodeConfig" specification.
- Node pool may contain one or many nodepool.
- Each node in the pool has a kubernetes node label "cloud.google.com/gke-nodepool: *node-pool-name*"
- When we create cluster the number and type of nodes that you specify becomes the default node pool. later we can add custom node pool of different sizes and types.
- **use case** attaching different node pool helps you to manage the cluster  efficiently by scheduling application based on resources. This optimizes the resource utilization.
- we can create upgrade and delete noe pools individually without affecting the cluster using "gcloud container node-pools"
- By default al new node pools run the latest stable version of kubernetes, existing node pool can be manually upgraded or automatically upgraded.

### Choosing a minimum CPU platform

While creating a cluster or a node pool, we choose a baseline minimum CPU platform for its nodes.

**Why this is required?** - as advance compute intensive workload in graphics, gaming and analytics industries can make use of the specific features available through different CPU capabilities. By providing minimum CPU platform workload can realize these gains in a more predictable manner and can ensure that your never use a CPU platform inappropriate for their workloads.

**Certain scenario when minimum CPU platform is not possible to create** 1. CPU platform is older than Zones default platform OR CPU platform no longer available and there is a newer CPU platform available at same cost *GKE will automatically create teh cluster or node pool using the newer platform*; 2. if CPU platform isn't available and there is no equivalent that is newer or identically priced, cluster or node creation fails. *Note: GKE will never use a CPU platform, which older OR costlier then the one mentioned. Also the node continue to run on CPU platform until the platform expires, then its moved to newer platform version*

> Check CPU platform is available: gcloud compute zones describe compute-zone

## Multi-zonal or regional cluster

Very important: in multi-zonal or regional cluster the node-pools are replicated to those zones automatically for redundancy.

Deletion of node also deletes the nodes automatically.

## Connect to the cluster

by default if you have only one cluster it will automatically configure. However incase of multiple cluster we need to configure the kubectl.

```sh
gcloud container clusters get-credentials gke-k8s-cluster --zone europe-west2-c --project nice-beanbag-288720
```
