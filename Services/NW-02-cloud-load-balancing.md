# Cloud load-balancing

Load balancer are managed by google. so don't worry about scaling or managing them.

**when we VM auto scaling, how does customer reaches the application** - using cloud VMs.

Supports both TCP, UDP traffic, as well as HTTP/HTTPs.

One IP can direct traffic to any region around the world, supports cross region load balancing.

Also includes multi region failover.

They are very responsive to health of the application, failover etc.

## Type of load balancing

- Global Load balancing: Layer 7(application layer) load balancing. (HTTP(s))
- Global SSL Proxy: Layer 4 load balancing of non HTTPs SSL traffic based on load. Supported on specific port number.
- Global TCP Proxy: Layer 4 non SSL TCP traffic. supported on specific port number.
- Regional: Load balancing of any traffic (TCP and UDP). Supports any port number.
- Regional internal: Load balancing of traffic inside VPC. Use for the internal tiers of multi-tier application.
