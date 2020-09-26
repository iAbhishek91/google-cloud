# VPC for GKE

Create a VPC that are suitable for GKE.

- Define VPC, with 2 custom subnet.
- Create subnet with IP range and two additional IP range for pod and services.
- Define firewall rules to allow http(s) and ssh.
- Verify the default routes.

## Create VPC

name: abhi-vpc-gke
desc: .....
subnet creation: custom
subnet-1:
  name: abhi-london-1
  region: europe-west2
  ip-range: 10.1.128.0/20
  additional ip range: 10.1.192.0/20
  additional ip range: 10.1.224.0/20
subnet-2:
  name: abhi-london-2
  region: europe-west2
  ip-range: 10.2.128.0/20
  additional ip range: 10.2.192.0/20
  additional ip range: 10.2.224.0/20
access to private google service: no

## Create firewall

rule-1:
  ingress
  target: all in the network
  filter: ip address - 0.0.0.0/0
  protocols & port: tcp - 80, 443
rule-2:
  ingress
  target: all in the network
  filter: ip address - 0.0.0.0/0
  protocols & port: tcp - 22

## Validate the default routes

Route to internet:
  destination IP address: 0.0.0.0/0
  next hop: default internet gateway
Route to each of the subnet's IP range:
  destination IP add range: 10.1.128.0/20
  destination IP add range: 10.1.192.0/20
  destination IP add range: 10.1.224.0/20
  destination IP add range: 10.2.128.0/20
  destination IP add range: 10.2.192.0/20
  destination IP add range: 10.2.224.0/20

## Why this setup is special for kubernetes

As kubernetes *specially VPC-native cluster* which uses IP aliasing needs three IP ranges. One for nodes(VM instance), pods and services.
