# Google Kubernetes engine (Hybrid)

- These is Google's managed kubernetes cluster.
- production ready with HA and comes with SLA.
- GKE cluster can be customized
  - type of nodes (type of operating system and resource power)
  - network settings.
  - location type : zonal and regional (can manage for both master and worker nodes)
  - version of kubernetes
  - same capabilities as GCE (custom VM, local SSD, custom SSH, GPU) are extended, we can literally attach any GCE instance as node.
- master(control plane) are completely managed by kubernetes service.
- Node (worker nodes) are google compute engines. Once the cluster are created you can view the VMs under compute engine. These same VMs can also be viewed form K8s console. Google under the hood perform many features, so that we don't have to worry about actual infrastructure anymore:
  - node k8s version auto update as master version gets updated. If something goes wrong while updating(docker daemon dies, kubelet error) GKE automatically kill that instance  and automatically recreates a new node with new version.
  - node auto repair
- Google recommendation also known as **Node right size recommendation** which is machine learning feature built in within GCE, which help us to identify the over or under utilize resources and recommends actions to be performed.
- Based on data, use of preemptable VMs allows you to scale your infra capabilities by three times. And with kubernetes is it very easy (mostly when we use stateless containers)
- Regional clusters: read in detail in below sections.
- "k expose deployment my-deploy --port=80 --type=LoadBalancer" creates a network load balancer with a public IP address. Hence app in the k8s cluster can be accessed using the public IP.
- All the autoscaling "node auto scaling", "horizontal pod autoscaling" and "vertical pod auto scaling" are done by GCP and are optimized:
  - "k autoscale my-deploy --max=5 --min=2 --cpu=80" auto scale deployment easily.
  - also comes with **auto node repair**, **node auto scaling**, **node k8s version auto upgrade**. Autoscale is also performed based on custom metrics. Send the metrices to stack driver and auto scale can be performed on any stackdriver metrics.
  - Support of **vertical auto scaling** is still not a native feature of kubernetes as of 1.18. However we have horizontal pod autoscaling which is pretty straight-forward(based on resource utilization it can scale the number of pods). in case of vertical auto scaling based on the work loads, the pods are redeployed with scaled resource request and limits.

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
- Each node in the pool has a kubernetes node label **cloud.google.com/gke-nodepool: *node-pool-name**
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

By default clusters are created on a single zone. There are two problems: first if the zone goes down and second during upgrade there may be some glitches like API server goes down.

With multi-zone or regional cluster, the nodes are distributed on 3 different zones on same region. It give benefits of HA of the cluster as both nodes are master (as master are also deployed on all the three zones).

During upgrade we do upgrade of one at time, so that we always have the option of fall-back. Hence there is not chance of loosing access to k8s API server.

The replication happens with persistent disks as well, when we have regional the disk are also replicated with streaming replicas on. Hence if one zone goes down, we don't loose on data.

Very important: in multi-zonal or regional cluster the node-pools are replicated to those zones automatically for redundancy.

Deletion of node also deletes the nodes automatically.

## Connect to the cluster

by default if you have only one cluster it will automatically configure. However incase of multiple cluster we need to configure the kubectl.

```sh
gcloud container clusters get-credentials gke-k8s-cluster --zone europe-west2-c --project nice-beanbag-288720
```

## GKE on-prem and other cloud

This is a new feature of GKE - Anthos. Which allow you to connect the cluster available on premise or on other cloud.

## Networking and security in GKE

Nodes contains the pods. Nodes have their IP address on VPC(read GCP IP address), however the virtual IP on each pod are only routed or accessible with in the cluster.

Generally(natively) the traffic flow is something like this: User makes a request to the load balancers, the load balancer forwards the traffic to VM by masking the IP using NAT, then the IPtable on the VMs forwards the packets to the correct pods, where the pod may or may not exist on the same node in which the load balancer have forwarded traffic to. This creates lots of latency and network problems. Defined as **double hop problem**.

GCP provides a feature called **VPC Native POD IP address(IP aliasing)** where actual IP address is assigned to POd as well same as nodes. In this case load balancer can directly forward traffic to the pod directly instead of sending it to node first. This is basically **container native load balancing**.

**Internal load balancing** is to expose the apps with in the cluster to other services within GCP. Internal load balancing are not accessible externally.

**Cloud NAT** a scenario where your third party service is accessing the services deployed in the GKE cluster, they need list of IP address for white listing. Now how we we provide the IP address as everything is changing (nodes mainly). Under the hood using SDN we forward the packet to correct IP address and define a fixed IP for exposing the services. From outside it looks like the IP address never changes, but it just maps the fixed IP with the dynamic IPs of the server.

**Multi cluster ingress** which can route traffic to multiple cluster. We can choose the closest cluster for low latency and forward the traffic to that particular cluster.

## Security

**private cluster** are clusters are k8s cluster which do not have external IPs and its not open to users.

**master authorized network** only certain people authorized can login, not a random person on the internet can access it.

**Netpol** calico is used.

**kubernetes secrets** are not encrypted by default, but in GKE they are encrypted with customer managed keys.

**Binary authorization** images that are signed by authenticated user can only run the image on the cluster else other images will not run.

**Container registry and vulnerability scanning** built in feature in GCR.

## Monitoring and tools

**Stackdriver kubernetes monitor** it can monitor nodes, and kubernetes resources as well.

- to start stack driver monitoring, first check the "stackdriver kubernetes engine monitoring" is enabled or not in cluster details. "legacy stackdriver logging" & "legacy stackdriver monitoring" is disabled. We can modify this setting even after creating the cluster.
- the above configuration will start monitoring on stack driver. Stackdriver >> resources >> kubernetes engine.
- there are three views: INFRA | WORKLOAD | SERVICES

**CI/CD** use cloud build which is a serverless fully managed, with multiple build minutes for free.

**GKE Dashboard** is really powerful tools fo give deeper dive in the object, with a power of modification.

**Service broker** we can use kubernetes to use the GCP services, or other cloud services that are in use. It gives better integration with GKE.

**resource usage based on namespace and labels** use for monitoring.

## Istio

Its powerful tool can configure Istio in one click and very powerful where it can managed micro service based application.

Cloud run is also integrated with GKE and built on top of Istio.
