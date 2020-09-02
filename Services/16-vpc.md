# VPC

Virtual Private cloud - allow you to define a virtual private network on GCP. Or easy way to use default VPC provided.

**VPC are just like routing tables, which allow routing(forward traffic) b/w one instance to another with in the same network or across sub networks and between GCP zones without any external IP address**. No need to manage a routing table or a router, those are managed by GCP.

## Features

- control ingress and egress traffic.
- define firewall rules(using metadata tags), (no need to manage a firewall software its managed by GCP).
- segment the network
- categorize the resources using tags and apply firewall rules.
- how they are connected with internet.

## Connection between VPCs

- connection between VPCs are done using VPC peering.
- we can share and manage access b/w VPCs provided IAM, this is known as shared VPC.

## Scope

VPC have a global scope. and subnets are regional and spans several zones.

> NOTE: when we increase the subnet size of a custom VPC, assigned IP address of the Cloud compute engine are not effected.
