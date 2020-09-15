# VPC

>NOTE: Google uses a software defined network which is defined on top of optical fiber network.

Virtual Private cloud - allow you to define a virtual private network on GCP. Or easy way to use default VPC provided.

**VPC are just like routing tables, which allow routing(forward traffic) b/w one instance to another with in the same network or across sub networks and between GCP zones without any external IP address**. No need to manage a routing table or a router, those are managed by GCP.

> Note: VPC is software defined network, no hardware are used to create these networks.

## Features

- control ingress and egress traffic.
- fine grain networking policies with in GCP or GCP and on-premise network or b/w other cloud providers.
- define firewall rules(using metadata tags), (no need to manage a firewall software its managed by GCP).
- segment the network
- categorize the resources using tags and apply firewall rules.
- how they are connected with internet.
- VPC are securely connected in hybrid env using cloud VPN or cloud interconnect.

## Connection between VPCs

- Also VPC are logically isolated from each other.
- connection between VPCs are done using VPC peering.
- we can share and manage access b/w VPCs provided IAM, this is known as shared VPC.

## VPN gateway

Its easy to connect with Google VPC as they are global. VPN gateway allow us to connect on-premise VMs.

## Scope

VPC have a global scope. and subnets are regional and spans several zones.

> Subnet can be private or public. Resources under private subnet are not shared with outside world.
> NOTE: when we increase the subnet size of a custom VPC, assigned IP address of the Cloud compute engine are not effected.

## VPC objects

- GCP resources can be connected or isolate them from each other using VPC.
- VPC can also be defined as set of google manged networking objects:
  - **Project**
    - It associate objects and services with billing.
    - Each project by default have 5 n/w(shared or peered) as quota. Can request to upgrade.
  - **Networks**
    - this network do not have IP addresses ranges.
    - its a construct of all the individual IP address within that network.
    - Each network consist of multiple subnet where each subnet have a designated IP and region. Combination of all the IP forms a network.
    - Network are global and spans over all available regions *as defined in scope section above*.
    - Network contains one or many sub networks.
    - They comes in three different flavours:
      - **default**: provided by GCP for every project | One subnet per region(non overlapping CIDR blocks) | and common default firewall rules - this allow ingress traffic for ICMP, SSH and RDP. Also supports traffic internal to VPC for all protocols and ports. *For example: default network in my VPC has us-central1 with CIDR 10.128.0.0/20 and europe-west1 with CIDR 10.132.0.0/20 and asia-southeast1 with CIDR 10.148.0.0/20*
      - **auto mode**: Default network is a auto-mode network as its automatically created and managed by GCP. Each sub network gets a IP range allocation ranging from /20 to /16 CIDR. All the subnet fits with in 10.128.0.0/9 CIDR block, therefore when a new region becomes available Auto Mode network creates a subnet from the 10.128.0.0/9 block.
      - **custom mode** this network gives you complete control over the subnet and IP ranges. No default subnet are created | full control over IP ranges | regional IP allocation choose IP address from *RFC 1918*(private network) address space.
      IP address cannot overlap b/w subnet of the same network.
      - DNs is scoped with a network. VM name and IP address is registered with network scoped DNS.

      > NOTE: that auto mode network can be converted to custom mode network to take the benefits of custom mode. However reverse is not possible.

  - **Sub networks**: as discussed above sub network are regional. As each region have multiple zones, subnetworks can span over multiple zones on a same region. VMs can be on same subnet but on different zones and hence they can have single firewall rules.
    - Common to subnetwork design the first, second & second last, last IP address are reserved for network, subnet's gateway and broadcast and broadcast respectively. *4 reserved IP in each subnet IP ranges*.
    - Expanding CIDR of each subnet are allowed without disturbing the current network and its object. (means it can increase from 24 to 16). The restrictions are below
      - cannot overlap with other subnets within the same network.
      - must be inside RFC 1918 address space
      - can expand but cant shrink. Hence, undo of expansion is not allowed.
      - avoid large subnets: chances of collision increases when we deal with VPC peering or VPN gateway etc. And it become difficult to manage as well.
      - auto mode allow expansion only from 24 to 16, more than that one need to select custom mode by converting the network mode.
  - **Regions**
  - **Zones**
  - **IP addresses**
  - **VMs**
  - **Routes**
  - **Firewall rules**

## Internal and External IP

- Allocation of IP address from subnet to VMs are done be DHCP service.
- DHCP lease are renewed every 24 hours.
- Its mandatory to have a internal IP address.
- Assigning internal IP address can choose from the below three options:
  - Choose auto from the subnetwork (ephemeral)
  - Choose custom from the subnerwork (ephemeral)
  - Choose static

- External IP address are assigned from a pool (ephemeral) or from a reserved static IP address. *Note: Static IP address are charged separately. And if they are not assigned to a resource they are charged higher than allocated ones.*
- Also VM(OS) doesn't know external IP address (irrespective option ephemeral or static), it is mapped transparently to internal IP by VPC. You can verify by the same by issuing ifconfig command within the shell. 
- Its optional to have external IP address.
- Assigning external IP address can choose from the below three options:
  - none
  - choose static from the pool (ephemeral)
  -choose static

## Interconnection between object from networking perspective

Here we take a example to elaborate things:

- a project have 5 network
- VM1(us-east1) and VM2(europe-west1) belongs to same network And hence can communicate with each other even though they are in different region. Since they are in different region they belongs to different sub network.
- The communication between the VM1 and VM2 happens using internal IP address.
- VM3(us-east1) and VM4(us-east1) belongs to different network And hence they cant communication using internal IP addresses. They need to use their external IP address and communicate over internet via google edge routers(this are not public internet). It doesn't matter if they are in same network. They come with different billing and security configuration

## Creating a VPC network

- Name: abhishek
- Description: my first network
- Subnet creation mode: auto or custom (auto allocates IP ranges to each subnet): custom
- Add a subnet
  - name: london
  - region: europe-west2
  - IP range: 10.128.10.0/29 *this gives total of 8 address, out of which 4 are taken by GCP*
  - private google access: off *cost you more*
  - flow logs: off *cost you more*
- Dynamic routing rules
  - regional
  - No DNS policies

Refer: image VPC creation with subnet with custom network type for a region.

**Now we create VPC**:

- Create a instance template with custom network, the create instance group with 4 instance: Success
- Increase the instance number to 5: Fail
- Expand the Subnet from /29 to /28: Success
- Verify that the VM creation success.

Refer: the image VM-creation-pre-subnet-expansion and VM-creation-post-subnet-expansion

> Note: VPC cant be delete if they are referred by some resources like instance template or group etc.
