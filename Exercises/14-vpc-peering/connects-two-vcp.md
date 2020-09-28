# VPC peering

> NOTE: By default vms on same subnet can communicate using internal IP address. Test using ping

We want to achieve the same using VPC peering, ping each other using internal IP.

## Steps

### Create VM template >> group

Preemptive VM | no External IP | N1 f1-micro  >> # of instances 1 | eu-west2

Create the above MIG in both the project (default, abhi-vpc)

first VM: (nice-beanbag-288720) | 172.16.1.2 | eu-west2-c
second VM: (doctord-in-london) | 10.154.0| eu-west2-c

### Validate that ping do not work

- ssh in 10.154.0.31
- ping -c 2 172.16.1.2

ping failed

## Create VPC peering

- name: doctord-vpc-peering
- two project id: nice-beanbag-288720 | doctord-in-london
- network we wish to connect: doctord-peering | default

Make sure the network which is getting VPC peering should not have any IP overlapping. Due to this we have created a small network only with one subnet called "doctord-peering". All the CIDR of that network is with **172.16.X.0/24**.

As well we need to create the peering from both the project. This is important to share the routes between the network.

> NOTE: VPC peering can be done between two VPC on same project or on different project.

Once created peering is created, GCP takes couple of time to activate the network peering. This will be fully connected network (full mesh topologies). *Route to subnets in the peered network will be automatically created*.

## Validate the VPC peering

Validate the imported and exported routes.

## validate the VM can ping each other

- ssh in 10.154.0.31
- ping -c 2 172.16.1.2

ping passed

> NOTE if ping is failing make sure firewall rule allows SSH and ICMP
