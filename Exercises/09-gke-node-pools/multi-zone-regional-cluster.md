# Compare multi zone and regional cluster with multiple node pools

- Create a multi zone cluster with multiple node pools.
  - validate the network(subnet) of the VMs
  - masters created
- Create a regional cluster with multiple node pools.
  - validate the network(subnet) of VMs
  - masters created

## first cluster - multi zonal

name: *multi-zone-cluster*
location type: *zonal*
default location: *europe-west2-a | europe-west2-b*
number of node: *2*
preemptive
enable *vpc-native traffic*
network: *abhi-vpc-gke* with subnet *abhi-london-2*
pool-name: *first-pool*
series & machine type: *N1* | *G1-small*
pod and service IP are auto-managed by google

add second node pool
pool-name: *second-pool*
number of node: *1*
preemptive
series & machine type: *N1* | *G1-small*

### Validate the network of the VMs in multi zonal cluster

- Number of VMs: 6
- Worker node zones: eu-west2-a | eu west2-b
- four instance template is created:
  - *gke-multi-zone-cluster-first-pool-538749b8*
  - *gke-multi-zone-cluster-first-pool-5e467f59*
  - *gke-multi-zone-cluster-second-pool-4fg547f89*
  - *gke-multi-zone-cluster-second-pool-8gy547609*
- four managed & zonal instance group is created:
  - *gke-multi-zone-cluster-first-pool-538749b8-grp*
  - *gke-multi-zone-cluster-first-pool-5e467f59-grp*
  - *gke-multi-zone-cluster-second-pool-4fg547f89-grp*
  - *gke-multi-zone-cluster-second-pool-8gy547609-grp*
- ip addresses of zone of each compute engine instances:
  - *gke-multi-zone-cluster-first-pool-538749b8-clg5 | eu-west2-a | 10.1.128.6*
  - *gke-multi-zone-cluster-first-pool-538749b8-pjw5 | eu-west2-a | 10.1.128.5*
  - *gke-multi-zone-cluster-first-pool-5e467f59-rtw1 | eu-west2-b | 10.1.128.3*
  - *gke-multi-zone-cluster-first-pool-5e467f59-rw2d | eu-west2-b | 10.1.128.4*
  - *gke-multi-zone-cluster-second-pool-4fg547f89-am1d | eu-west2-a | 10.1.128.8*
  - *gke-multi-zone-cluster-second-pool-8gy547609-am1d | eu-west2-b | 10.1.128.9*
- six persistent disk is created, one for each VM in the same zone.

### Master details in multi zonal cluster

Only one master is create.
master node zone: eu-west1-a

## second cluster - regional

name: *regional-cluster*
location type: *region*
region: *eu-west2*
default location: *europe-west2-a | europe-west2-b*
number of node: *1*
preemptive
enable *vpc-native traffic*
network: *abhi-vpc-gke* with subnet *abhi-london-2*
pool-name: *first-pool*
series & machine type: *N1* | *G1-small*
pod and service IP are auto-managed by google

add second node pool
pool-name: *second-pool*
number of node: *1*
preemptive
series & machine type: *N1* | *G1-small*

### Validate the network of the VMs  in regional cluster

- Number of VMs: 4
- Worker node zones: eu-west2-a | eu west2-b
- four instance template is created:
  - *gke-multi-zone-cluster-first-pool-638749b8*
  - *gke-multi-zone-cluster-first-pool-6e467f59*
  - *gke-multi-zone-cluster-second-pool-5fg547f89*
  - *gke-multi-zone-cluster-second-pool-9gy547609*
- four managed & zonal instance group is created:
  - *gke-multi-zone-cluster-first-pool-638749b8-grp*
  - *gke-multi-zone-cluster-first-pool-6e467f59-grp*
  - *gke-multi-zone-cluster-second-pool-5fg547f89-grp*
  - *gke-multi-zone-cluster-second-pool-9gy547609-grp*
- ip addresses of zone of each compute engine instances:
  - *gke-multi-zone-cluster-first-pool-638749b8-clg5 | eu-west2-a | 10.1.128.6*
  - *gke-multi-zone-cluster-first-pool-6e467f59-rtw1 | eu-west2-b | 10.1.128.3*
  - *gke-multi-zone-cluster-second-pool-5fg547f89-am1d | eu-west2-a | 10.1.128.8*
  - *gke-multi-zone-cluster-second-pool-9gy547609-am1d | eu-west2-b | 10.1.128.9*
- six persistent disk is created, one for each VM in the same zone.

### Master details in regional cluster

Two master is create:
master node zone: eu-west1-a | eu-west2-b

**GOLDEN RULE** Each node pool is used to deploy similar type of nodes on single zone. Number of node defines in node-pool will be multiplied(replicated) in case of multi zone and regional clusters.
