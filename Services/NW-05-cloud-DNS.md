# Cloud DNS

> 8.8.8.8 is worlds free DNS service provided by Google.

Similarly for internal DNS, for the application that we build and deploy in GCP are supported by Cloud GCP.

- These DNS servers are **managed** by Google
- HA (100% SLA) with low latency, scalable and cost effective.
- DNS servers are programmable, hence we can use GCP SDK, Gcloud to define millions of DNS records.
- Cloud DNs are hosted on same infra as Google. Its used for www.google.com as well. It uses the same google network.

## DNS resolution for both internal and external

- Each instance has a hostname that can be resolved to an internal IP address. Host name is the VM. (There are two hostname associated) - use **hostnamectl** command
  - Static hostname: debian
  - Transient hostname: instance-1
- FQDN: hostname.zone.c.project-id.internal
- internal DNS resolver  (this are known as metadata server) helps to configure the compute engine (169.254.169.254). Try **ping 169.254.169.254**. This are used by GCP internally.
- When a instance is recreated with same name, the DNS updates the IP address and points ot instance.
- internally a lookup table is used to map internal address with external addresses.
- They are configured for use on instance via DHCP.
- Provides answer for internal and external address.

- instances with external IP address can allow connections from hosts outside the projects.
  - user can directly connect directly using external IP address.
  - admins can also publish public DNS records pointing to the instances. Public DNs records are not published automatically.
- To publish the external IP of the instance we can either use existing DNS server of the company - outside GCP.
- DNS zone can be hosted using cloud DNS.

## Alias IP ranges

It allow one to assign a rance of IP addresses as alias to a VM's network interface using alias IP ranges.

**Use cases**: we can assign IP addresses to each services running or a VM. or Container running on a VM. In that case we can directly speak with the service using the IP addresses.

The Alias IP range are drawn from the subnets IP address. Subnet can have primary IP range and secondary IP ranges. and alias IP ranges can be drawn from any of the group.

Primary CIDR range or Secondary CIDR range.
