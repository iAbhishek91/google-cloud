# Internal TCP load balancer

- Creates VPC
- Create 2 sub-net within a region - internal load balancer works with in a region.
  - 1 with 10.10.10.0/24
  - 2 with 10.10.20.0/24
- Create firewall rules to allow,
  - SSH,
  - Http
  - Load balancer health check: allow TCP:80 from 130.211.0.0./22 and 35.191.0.0/16 (for specific network tag)
  - allow internal traffic: allow everything from 10.10.0.0/16 (for specific network tag)
- Create NAT so that the VMs can communicate with the Internet
- Create instance template
  - 1 with the network tag, no ext IP, on 1st subnet
  - 2 with the network tag, no ext IP, on 2st subnet
- Create instance group with auto scale
- Create a new instance called "tes". This vm can lie in any VM setup.
- Create load balancer > TCP > only between VM > Backend: MIG-1 and MIG-2 > Frontend: any subnet | IP static(10.10.30.7) | port 80 |
- test the connection using curl to loadbalancer IP address.
