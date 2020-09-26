# Public Cluster

Analyse network aspect of public cluster.

- Analyse the Subnet that is assigned to GKE.
- Analyse Public cluster works when VPC peering is disabled.
- Find the API server URL of a cluster, and find the IP.

## Subnet

Network: abhi-vpc-gke
Subnet: abhi-london-1
Enable VPC-native traffic routing: true
Automatically create secondary ranges: false
Pod secondary IP address: pod(10.1.192.0/20)
Service secondary IP address: service(10.1.224.0/20)

## Analyse public cluster works fine with VPC peering disabled

Cant disable as restricting VPC is an organization policies. However we can validate in the next section that the IP are external and NOT internal. IP peering.

## API server URL

*the below is taken from kubeconfig*:

- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://35.230.139.157
  name: gke_nice-beanbag-288720_europe-west2-b_sandbox
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://35.189.74.170
  name: gke_nice-beanbag-288720_europe-west2-c_gke-k8s-cluster
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://34.105.200.134
  name: gke_nice-beanbag-288720_europe-west2-c_sandbox

All the above IP are not in RFC 1918 and hence they are all external IP. This confirms that all public cluster uses external IP to connect with the nodes.
