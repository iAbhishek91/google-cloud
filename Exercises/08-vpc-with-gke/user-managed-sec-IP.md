# Show how to manage secondary IP manually

- Create a vpc for GKE (done: create-vpc-for-GKE.md)
- Create a Cluster using the same network
- Don't use auto manage secondary IP in network section
- Validate IP addresses of pod and services.
- Validate the IP address of the nodes

## Create a cluster

*All details will be same only in network tab we need provide the info about the custom network and user manged secondary IP addresses*.

Public cluster.
Network: abhi-vpc-gke
Subnet: abhi-london-1
Enable VPC-native traffic routing: true
Automatically create secondary ranges: false
Pod secondary IP address: pod(10.1.192.0/20)
Service secondary IP address: service(10.1.224.0/20)
*leave everything with default*.

Click create.

## Validate the pod and services IP address

Login to cluster from gcloud

```sh
# very imp command to get the kubeconfig file to connect to cluster
gcloud container clusters get-credentials sandbox --zone europe-west2-b --project nice-beanbag-288720

k get all -n kube-system -o wide
## OUTPUT
## pods backed by deployments. IP address are taken from 10.1.192.0/20
# pod/event-exporter-v0.3.0-5cd6ccb7f7-mtdfd     2/2     Running   10.1.192.8   gke-sandbox-default-pool-b32895b7-99sp
# pod/fluentd-gcp-scaler-6855f55bcc-tzg89    1/1     Running   10.1.192.7    gke-sandbox-default-pool-b32895b7-99sp

## pods backed by daemon sets. IP address are taken from 10.1.128.0/20
#pod/fluentd-gcp-v3.1.1-7c2g4           2/2     Running   10.1.128.2    gke-sandbox-default-pool-b32895b7-99sp

## Services. IP address are taken from 10.1.224.0/20
service/default-http-backend   NodePort    10.1.239.31
service/heapster               ClusterIP   10.1.228.248
service/kube-dns               ClusterIP   10.1.224.10
service/metrics-server         ClusterIP   10.1.238.4  
```

## Validate the IP address of VM instances

*10.1.128.2* this is assigned to the VM.
