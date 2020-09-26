# Public Cluster

Analyse network aspect of private cluster.

- Analyse the Subnet that is assigned to GKE.
- Analyse Private cluster works when VPC peering is enabled.
- Find the API server URL of a cluster, and find the IP.

## subnet

Network: abhi-vpc-gke
Subnet: abhi-london-1
Master IP address: 172.16.128.0/28
Enable VPC-native traffic routing: true (readonly)
Automatically create secondary ranges: false
Pod secondary IP address: pod(10.1.192.0/20)
Service secondary IP address: service(10.1.224.0/20)

## Analyse Private cluster works with VPC peering enabled

It workes, we are not able to restrict VPC peering as this is organization level change and we don't have organization defined in our project.

## Find API server URL of a cluster

The below IP address is used as control-plane IP to connect with kubernetes API server.

- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://172.16.128.2
  name: gke_nice-beanbag-288720_europe-west2-b_sandbox-private
