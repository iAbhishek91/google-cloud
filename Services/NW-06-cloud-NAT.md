# Cloud NAT

NAT allows compute engine and kubernetes pod and services to communicate with internet using a public and shared IP addresses.

NAT do not allow access of internal services from internet. In another words, NAT only deals with egress traffic.

## Create a NAT

- Name: doctord-nat
- VPC network: abhi-vpc-gke
- Region: europe-west2
- Cloud router: doctord-router
- NAT mapping
  - source(internal): only primary IP ranges.
  - NAT IP address: Automatic
  - Destination(read only): Internet
