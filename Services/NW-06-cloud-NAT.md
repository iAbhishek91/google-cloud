# Cloud NAT

NAT allows compute engine and kubernetes pod and services to communicate with internet using a public and shared IP addresses.

NAT internally uses a NAT gateway to connect with the **cloud router** and the router connects with the internet via the internet gateway of the subnet.

NAT do not allow access of internal services from internet. In another words, NAT only deals with egress traffic.

NAT also uses *Andromeda*. This means this no proxy(extra hop) in the network. *Traffic are directly passed onto the internet.*

## Create a NAT

- Name: doctord-nat
- VPC network: abhi-vpc-gke
- Region: europe-west2
- Cloud router: doctord-router
- NAT mapping
  - source(internal): only primary IP ranges / or primary or secondary ranges.
  - NAT IP address: Automatic / manual
  - Destination(read only): Internet
