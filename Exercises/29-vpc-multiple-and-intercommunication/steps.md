# Multiple VPC and interconnection

In this lab, you will learn how to perform the following tasks:

Create custom mode VPC networks with firewall rules
Create VM instances using Compute Engine
Explore the connectivity for VM instances across VPC networks
Create a VM instance with multiple network interfaces

## Steps

### Step-1: Create the VPC

Create two custom networks **managementnet** and **privatenet**, along with firewall rules to allow **SSH**, **ICMP**, and **RDP** ingress traffic.

```sh
# create a network
gcloud compute networks create privatenet --subnet-mode=custom

# create a sub network
gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-central1 --range=172.16.0.0/24

# View the network
gcloud compute networks list

# View all the sub-net from all the network and sorted by network name
gcloud compute networks subnets list --sort-by=NETWORK
```

### Step-2: Create firewall rules

```sh
# create firewall rule
gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

# list all the firewall rules, sorted by network
gcloud compute firewall-rules list --sort-by=NETWORK
```

### Step-3: Create VM instance

```sh
# Create VM
gcloud compute instances create privatenet-us-vm --zone=us-central1-c --machine-type=n1-standard-1 --subnet=privatesubnet-us

# List all the VMs, sorted by ZONE
gcloud compute instances list --sort-by=ZONE
```

- Post this step, VM in same VPC should be able to ping each other using internal IP, but not others.

#### Step-4: Create a VM with multiple network interface

> NOTE: The number of interfaces allowed in an instance is dependent on the instance's machine type and the number of vCPUs. The n1-standard-4 allows up to 4 network interfaces. Refer here for more information.

Its easy just select multiple interface instead of one, while creating a VM or later.

- VM is a regional resource
- If a VPC have a subnet created on that region, we can assign that to the VM.

Name: multiple-interface
Series: N1
Machine Type: 4 vCPUs (n1-standard-4)
Add multiple subnet from different VPC

### Step-5: Test

Instances cant communicate with other VM in the same VPC, but other subnet, until explicitely specified.

In a multiple interface instance, every interface gets a route for the subnet that it is in. In addition, the instance gets a single default route that is associated with the primary interface eth0. Unless manually configured otherwise, any traffic leaving an instance for any destination other than a directly connected subnet will leave the instance via the default route on eth0.

```sh
# check the routes
ip route
# default via 172.16.0.1 dev ens4
# 10.128.0.0/20 via 10.128.0.1 dev ens6
# 10.128.0.1 dev ens6 scope link
# 10.130.0.0/20 via 10.130.0.1 dev ens5
# 10.130.0.1 dev ens5 scope link
# 172.16.0.0/24 via 172.16.0.1 dev ens4
# 172.16.0.1 dev ens4 scope link
```
