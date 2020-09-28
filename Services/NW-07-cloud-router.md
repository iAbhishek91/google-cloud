# Cloud Router

This service can't be used by user directly. Its required/recommended by the below services

- Cloud NAT (required)
- Cloud Interconnect (required)
- Classic VPN (recommended)

Cloud router is managed, scalable, distributed service that programs dynamic routes. It works with both legacy and VPC network.

Use case: *When you extend your on-premises network to Google Cloud, use Cloud Router to dynamically exchange routes between your Google Cloud networks and your on-premises network. Cloud Router peers with your on-premises VPN gateway or router. The routers exchange topology information through BGP.*

Topology changes automatically propagate between your VPC network and your on-premises network. When using Cloud Router, you don't need to configure static routes.

## Create a router

Cloud router takes a name: doctord-router, network: abhi-vpc-gke, region: europe-west2 (London).
