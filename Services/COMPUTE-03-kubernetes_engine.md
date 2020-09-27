# Google Kubernetes engine (Hybrid)

- These is Google's managed kubernetes cluster. (all the kubernetes components are managed including kubelets on worker node)
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
> NOTE: GCP uses containerD as container runtime

## Master

- Kubernetes master are managed by GKE. The k8s master VM are launched under Googles' own  project. *Both the infra(VMs) and the master components like - kube-scheduler, api-server, control-manager, etcd, and kubelet*
- The master k8s VM run on googles project's VPC. The nodes are using user's VPC, hence the cluster works with external IP of the VMs. **However in case of private cluster VPC peerings is used to create the cluster**. Refer exercise: VPC with GKE.
- We can just mention the geographical location of the master*probably nearest possible location from the worker nodes*
- One component is extra than vanilla kubernetes is - kube cloud manager *this brings in GCP features to GKE k8s cluster*
- also you are **not billed** for master infra.
- **Auto upgrade** depends on "master version" cluster configuration. It can be *release channel* or *static version*. if its static, then cluster admin need to manually upgrade the cluster. however if its configured as *release channel* then GKE auto upgrade k8s version for us.

## Cluster Auto scaler

Auto resize your cluster node-pool based on demand. When workload is high, auto scaler will add nodes to the node-pool, and vice-versa.

> NOTE: Do NOT switch on auto-scaling on MIG, as autoscaling in compute engine and GKE are different.

This is recommended as it will increase availability and effective cost managements.

**How it works ?**
Auto scaling works on per node-pool basis. GKE also takes care of cost of auto-scaling and it will automatically choose the cheapest option available.

The auto scaling takes place based on resource request than actual utilization. Auto scaler periodically checks the status and takes decision.

- if pod are unscheduled due to not enough nodes in the node pools, and max limit of auto scaler is not reached, new nodes will be added.
- if nodes are under utilized and all pods are scheduled even with fewer nodes in the node pool it will auto delete.

Manual changes & labels added after creation are not tracked, and will be lost in auto scaling.

**Multi zonal/regional cluster with auto scaling**, will evenly scale up in all the zones. However while scale down it will only scale down in the current zone. This creates uneven distribution uneven.

**Auto scale profile** whole purpose is to utilize resource in optimized way, but availability is compromised. New workload need to wait for scale up. For this trade off profile is introduced. There are two profile: *balanced* by default and *optimization-utilization*(this is not suggested for use).

**Best Practice**
Workload of a auto scale cluster should be able tolerate fault. *Common scenario: If you have one replica of a workload running on the cluster, the pod will be rescheduled to other nodes if the node is deleted. And this will create disruption*.

> NOTE: While a cluster is under going autoscaling, if workloads are deleted at the same time then there might be transient disruption.

## Vertical Pod auto scaling

Horizontal pod auto scaling is provided by K8s as a resource, which allow pod to auto-scale based on cpu and memory. This will increase the number of replicas.

however pod Vertical auto-scaling is adjusting resource request an limits of pod. PodDisruptionBudget are recommended to be configure in the cluster.

**Advantages**
Cluster resources re efficiently utilized as request and limits are close to actual.
Also pods are scheduled on correct node.
Maintenance time reduced.

**Limits**
500 pod are supported *VerticalPodAutoscaler* per cluster.
supported on regional cluster.
Don't combine horizontal and vertical auto scaling on cpu and memory.
JVM based workload are not supported.

**How it is achieved**: resource request and limits cant be changed on existing pod due to limitation of k8s. So GKE will evicts the pod and recreates it.

## API thats need to be enabled for GKE

Google Kubernetes Engine API
and Google container registry API

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

- node pool is **NOT a K8S feature** its something provided by GKE to better manage the worker nodes.
- Node pool is group of nodes, that have same configuration.(they are like manged instance group in compute engine)
- Node pool uses "NodeConfig" specification.
- Node pool may contain one or many VMs.
- Each node in the pool has a kubernetes node label **cloud.google.com/gke-nodepool: *node-pool-name**
- When we create cluster the number and type of nodes that you specify becomes the default node pool. later we can add custom node pool of different sizes and types.
- **use case** attaching different node pool helps you to manage the cluster  efficiently by scheduling application based on resources. This optimizes the resource utilization.
- we can create upgrade and delete node pools individually without affecting the cluster using "gcloud container node-pools"
- By default all new node pools run the latest stable version of kubernetes, existing node pool can be manually upgraded or automatically upgraded.
- Each node pool is deployed in **only one zone**. In case multi zone or regional cluster the node pool is replicated.
  - each node pool creates a image template, from which managed & zonal image group is created.
  - each image group gives birth to instance in a single zone.
  - each vm will have separate persistent disk in the same region where the VMs are.
- **node images** are OS images thats run on each nodes. We can upgrade the disk after it is created.
- Specific node images that are commonly used:
  - *container - optimized OS*: based on Linux kernel and optimized to enhance node security. Its is backed by google engineers for any patches or upgrades. Better that all other image in terms of support, stability and security.
  - *Ubuntu*: It matches the GKE node image requirement. Use Ubuntu only if you need support of XFS, CephFS or Debian packages.
  - *Windows server LTSC & SAC*: Long term support channel and semi annual channel.
  - *containerd*: it comes with two flavor *cos-containerd* & *ubuntu-containerd*. Both the image have containerd as the runtime and directly integrated with kubernetes.
  - storage driver ext4 is supported by cos and ubuntu. Additionally ubuntu supports XFS and CephFS.

>NOTE: node pool are specific for GKE and if you dont have a cluster you cant create a node pool. As node pool needs a cluster name while creating.

## Shielded VM

These VMs are more secure and google makes sure **below restriction** are in place:

- Every node in the cluster is a VM running in Google's data center.
- Every node is part of the managed instance group provisioned for the cluster.
- The kubelet is being provisioned a certificate for the node on which it is running.

**Availability**:

- Shielded GKE nodes are available in all regions and zones.
- Shielded GKE nodes are available in GKE 1.13.6-gke.0 and higher.
- Can be used with Container-Optimized OS (COS), COS with containerd, and Ubuntu node images.
- Can be used with GPUs.

**Upgrade or disable shielded VM feature**:

- we can convert a existing cluster into a shielded VM cluster.
- GKE will re-create master and nodes as shielded. There will be a downtime. Note: re-creation will not happens if its between maintenance window.

- if you are disabling, same happens. The VMs are recreated as ordinary VM and there will be downtime.

**shield options**: These are node-pool options. They are independent of each other and can be configured individually.

- *Enable integrity monitor*
- *Enable secure boot*: when enable third party unsigned kernel modules can be loaded, hence its disabled by default. If one is not using 3rd party modules its recommended to enable this settings.

```sh
# cluster creation time
gcloud container cluster create cluster-name --shielded-secure-boot

# node pool creation time
gcloud container node-pool create pool-name --shielded-secure-boot
```

**Caveat**:

- shield node is a cluster level configuration, once we enable this flag, any nodes created in a node pool without Shielded GKE Nodes enabled or created outside of any node pool will NOT be able to join the cluster.

### Choosing a minimum CPU platform

While creating a cluster or a node pool, we choose a baseline minimum CPU platform for its nodes.

**Why this is required?** - as advance compute intensive workload in graphics, gaming and analytics industries can make use of the specific features available through different CPU capabilities. By providing minimum CPU platform workload can realize these gains in a more predictable manner and can ensure that your never use a CPU platform inappropriate for their workloads.

**Certain scenario when minimum CPU platform is not possible to create** 1. CPU platform is older than Zones default platform OR CPU platform no longer available and there is a newer CPU platform available at same cost *GKE will automatically create teh cluster or node pool using the newer platform*; 2. if CPU platform isn't available and there is no equivalent that is newer or identically priced, cluster or node creation fails. *Note: GKE will never use a CPU platform, which older OR costlier then the one mentioned. Also the node continue to run on CPU platform until the platform expires, then its moved to newer platform version*

> Check CPU platform is available: gcloud compute zones describe compute-zone

## Type of cluster based on availability

### Zonal cluster

- single control-plane, in a single zone *managed by GKE(with SLA), so don't worry about the HA of control plane*
- there are two type of zonal cluster
  - single zone ( control-plane and nodes are on the same zone)
  - Multi Zone ( single control plane, with nodes distributed on multiple zones)

> NOTE: If your requirement is to maintain the capacity of the cluster(node pools), regional cluster is perfect. Since capacity are disrupted when there is a zonal failure.

### Regional cluster

There are two problems: first if the zone goes down and second during upgrade there may be some glitches like API server goes down.

With regional cluster, by default the entire cluster(master, node, pd) are replicated on 3 different zones on same region (this number can obviously changed). It give benefits of HA of the cluster as both nodes are master (as master are also deployed on all the three zones).

During upgrade we do upgrade of one cluster at time, so that we always have the option of fall-back. Hence there is not chance of loosing access to k8s API server.

The replication happens with persistent disks as well. For regional cluster, the disk are also replicated with streaming replicas on. Hence if one zone goes down, we don't loose on data.

Very important: in multi-zonal or regional cluster the node-pools are replicated to those zones automatically for redundancy. Deletion of node also deletes the nodes automatically. hence we can conclude by saying that in regional cluster each zone have same number of worker nodes. This feature impact on the cost.

> NOTE: A cluster created as zonal cluster cant be modified into regional cluster or vice versa.
> By Default region consist of 9 nodes, (3 node * 3 zone), and by default there are only 8 IP/region. So first we need to increase if you go with all default settings.

## Type of cluster based on version

### release channel (recommended by Google)

- **Auto upgrade** depends on "master version" cluster configuration. It can be *release channel* or *static version*. if its static, then cluster admin need to manually upgrade the cluster. however if its configured as *release channel* then GKE auto upgrade k8s version for us.
  - There are three version of auto upgrade: *each channel are trade off b/w availability and update churn*
    - *rapid*: get latest version of k8s asap. Cluster is frequently upgraded.
    - *regular*(default): 2-3 months after releasing in rapid. It provides perfect balance between feature availability and release stability ans is recommended by Google.
    - *Stable*: 2-3 months after release in regular. is the last one hence features are available at last, but cluster are less frequently upgraded.
  - Critical security patches are released to all channels immediately.
  - Each channel has a default version which will be selected automatically. Google recommends to test the version before auto-upgrade. *Prevent yourself from version upgrade disruption*.
    - how to test the release version before its auto upgrade: in Q&A.
  - update channels of existing cluster:
    - upgrade: to one version is allowed. *stable to regular is allowed, however stable to rapid is not allowed.*
    - downgrade: not allowed, as it may result in downgrading k8s versions. *rapid to regular, regular to stable*
  - Nodes are automatically upgraded to recommended version based on the channel.
  - By default upgrade may occur any time in the day. But its suggested to define **maintenance window and exclusion**. They both are independent of each other and can be defined separately.
    - **maintenance window**: Repeatable window when upgrade can happen.
      - There are different types: off-peak, on-call, multi cluster.
      - At least 24 hours of period within a span of 14 days.
      - Example: starting from 12 midnight a duration of 24 hours on saturday.
    - **maintenance exclusion**: is a time period when upgrade will be paused. There can be 3 exclusion time period allowed. Make sure you provide enough time to Google for upgrading the version. Not repeatable window.
    > NOTE the caveats of **maintenance window and exclusion**: GKE reserves the right to override maintenance policies for critical security vulnerabilities. and they don't have any impact on other service upgrade. *they are only meant for kubernetes version upgrade.

### default

Uses the default version of GKE and changes overtime. At the time of creation it selects the default version and admin needs to upgrade to next version when available.

### Static version

you manage the version and upgrade.

### alpha cluster

-- DO NOT USE FOR PRODUCTION --

Alpha cluster are for experimenting with alpha features of kubernetes. They are normal GKE cluster with some restriction. It runs the current default version of k8s, alternatively we can choose the different version.

> NOTE: if doesn't matter which version of k8s you are running on alpha cluster, the Alpha API are enabled.

**Common scenario**: for advance users to experiment on k8s features. these cluster are short lived.

**Limitation of alpha cluster**:

- cant be upgraded
- do not receive security patches.
- short lived, auto deleted after 30 days.
- Do not follow GKE SLA *for example up time of 99%*
- auto upgrade and auto repair will be disabled, hence we cant choose release channel.

**Alpha GKE version** This are new version of k8s built on top of open source k8s to support GKE features to its optimal. Its not necessary to that alpha cluster runs alpha GKE version.

## Type of cluster based on n/w communication between pods

Default cluster mode depends on how the cluster is created. But the below can be changed.

- from console: VPC-native cluster
- from REST API: Route based cluster
- from gcloud:
  - v256.0.0 and higher or v250.0.0 and lower: Route based
  - else: VPC native cluster

Updating of network type or IP address is NOT possible, once cluster is created.

### VPC-native cluster

- It uses alias IPs.
- VPC network is required. *legacy network cant be used*

For VPC native cluster: a subnet is required from the VPC network. There are three different subnet or IP ranges are used from the given subnet.

- Node IP: primary IP address range from the subnet.
- Pods IP: are taken from secondary IP address ranges of the subnet. GKE allocates /24 CIDR (256 IP address) for pods IP per node. 110 pods/node are supported from the 256 IP addresses. Extra IPs are used to mitigate IP address reuse as pods are added or deleted from the node.
-Service IP(also known as ClusterIP): cluster IP addresses are taken from the another secondary IP address ranges of the subnet.

> NOTE: IP ranges for node, pod and network should NOT overlap. Also the range of IP should fall under RFC-1918.

Creating secondary IP address to VPC subnet. There are two ways

- Managed by GKE(by default): GKE will create and manage the IP ranges for you. User just need to provide the CIDR *for eg: 10.1.0.0/16 pod or 10.2.0.0/20 for service* or we can also mention the subnet mask only *for eg: /16 and /20 for pod and service respectively*
- User managed: Create the secondary ranges in the subnet and then create the cluster. Refer: example/08-vpc-with-gke

> Also if we don't provide the secondary address for the pod, it will automatically calculate based on the **maximum pod per node** under network section.

There are certain restriction if VPC-native cluster is created on top of shared VPC.

### Route based cluster

- Cluster that uses Google cloud routes are known as route based cluster. Need to read.

## Type of cluster based on n/w isolation

### Private Cluster

Private cluster allow you to isolate nodes *only nodes not GKE cluster as whole* from having inbound and outbound connectivity to public internet.
Nodes do not have external IP assigned. In case outbound connectivity is required we need to connect use cloud NAT or manage NAT gateway ourself.

Even though the node IP addresses are private, external clients can reach Services in your cluster. For example, you can create a Service of type LoadBalancer, and external clients can call the IP address of the load balancer. Or you can create a Service of type NodePort and then create an Ingress. GKE uses information in the Service and the Ingress to configure an HTTP(S) load balancer. External clients can then call the external IP address of the HTTP(S) load balancer.

VPC-native traffic routing is required for private network.

Access to master is disabled by default. There is a external IP address assigned to master node, however its only for googles internal use for cluster management.

Master IP range is required to configure the IP range. Make sure this **IP falls under RFC 1918** and **do NOT overlap with any subnet IP ranges** as this will VPC peering. Only CIDR /28 range is allowed. *class-c(172.16.0.0) range is suggested by google*

**Private google cloud** is enabled by default. Hence private nodes and workload have limited access to internet. It can access google APIs and other services over Googles private network.

### Public Cluster

By default, it exposes its application to internet.

## Connect to the cluster

by default if you have only one cluster it will automatically configure. However incase of multiple cluster we need to configure the kubectl.

```sh
gcloud container clusters get-credentials gke-k8s-cluster --zone europe-west2-c --project nice-beanbag-288720
```

## Cluster multi tenancy

>NOTE: its nothing from implementation side, just that it is shared between different teams and resource with different requirements.

A single cluster can be shared by different users within same organization. Its a alternative to managing multiple single tenancy cluster. "Tenants" are user or workload.

GKE makes sure that there are not malicious tenant which impacts other tenants.

**Consideration**
When you are planning for multi-tenancy cluster you should make sure a layer of resource segregation in the cluster, node, ns, po, node or containers. Also consider the security implication of sharing resources.

**Advantages**
easy maintenance, less resource fragmentation, and no time to give access to new tenant.

## GKE on-prem and other cloud

This is a new feature of GKE - Anthos. Which allow you to connect the cluster available on premise or on other cloud.

## Networking

Nodes contains the pods. Nodes have their IP address on VPC(read GCP IP address), however the virtual IP on each pod are only routed or accessible with in the cluster.

Generally(natively) the traffic flow is something like this: User makes a request to the load balancers, the load balancer forwards the traffic to VM by masking the IP using NAT, then the IPtable on the VMs forwards the packets to the correct pods, where the pod may or may not exist on the same node in which the load balancer have forwarded traffic to. This creates lots of latency and network problems. Defined as **double hop problem**.

GCP provides a feature called **VPC Native POD IP address(IP aliasing)** where actual IP address is assigned to POds and services as well same as nodes. In this case load balancer can directly forward traffic to the pod directly instead of sending it to node first. This is basically **container native load balancing**.

**Internal load balancing** is to expose the apps with in the cluster to other services within GCP. Internal load balancing are not accessible externally.

**Cloud NAT** a scenario where your third party service is accessing the services deployed in the GKE cluster, they need list of IP address for white listing. Now how we we provide the IP address as everything is changing (nodes mainly). Under the hood using SDN we forward the packet to correct IP address and define a fixed IP for exposing the services. From outside it looks like the IP address never changes, but it just maps the fixed IP with the dynamic IPs of the server.

**Multi cluster ingress** which can route traffic to multiple cluster. We can choose the closest cluster for low latency and forward the traffic to that particular cluster.

**kubernetes services**:

- same as vanilla kubernetes services.
- it has stable endpoints to connect the multiple ephemeral Pod hosting same service.
- *ClusterIP* its host the service accessible only within the cluster. (same as vanilla k8s)
- *NodePort* expose the service on a specific port on all the cluster nodes. (same as vanilla k8s)
- *LoadBalancer* exposes service externally via load balancer. Load balancer give you access to regional network. The service can be accessed via network loadbalancer's IP.

## Security

**private cluster**:

- its not open to all users. They are hidden from the public internet.
- they are accessed by GCP services like stack driver using internal IP.
- authorized network (IP ranges that are allowed to access the master)can have access to the cluster using external IP.
- both zonal an regional cluster can be created as private cluster.

**master authorized network** only certain people authorized can login, not a random person on the internet can access it.

**Netpol** calico is used.

**kubernetes secrets** are not encrypted by default, but in GKE they are encrypted with customer managed keys optionally. encrypt Secrets at the application layer using a key you manage in Cloud KMS.

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
