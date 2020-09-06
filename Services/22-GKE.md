# Google Kubernetes engine

- These is Google's managed kubernetes cluster.
- production ready with HA and comes with SLA.
- GKE cluster can be customized
  - type of nodes (type of operating system and resource power)
  - network settings.
- Node (controlplane and worker nodes) are google compute engines. Once the cluster are created you can view the VMs under compute engine. These same VMs can also be viewed form K8s console.
- "k expose deployment my-deploy --port=80 --type=LoadBalancer" creates a network load balancer with a public IP address. Hence app in the k8s cluster can be accessed using the public IP.
- "k autoscale my-deploy --max=5 --min=2 --cpu=80" auto scale deployment easily.
- also comes with **auto node repair**, **auto scaling**, **auto upgrade**.

## API thats need to be enabled for GKE

Google Kubernetes Engine API
and Google Artifact registry API