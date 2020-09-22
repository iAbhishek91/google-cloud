# VPC

>NOTE: Google uses a software defined network which is defined on top of optical fiber network.

Virtual Private cloud - allow you to define a virtual private network on GCP. Or easy way to use default VPC provided.

**VPC are just like routing tables, which allow routing(forward traffic) b/w one instance to another with in the same network or across sub networks and between GCP zones without any external IP address**. No need to manage a routing table or a router, those are managed by GCP.

> Note: VPC is software defined network, no hardware are used to create these networks.

Here we discuss about network, subnet, IP address, DNS (refer DNS.md), routes and firewall rules.

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

> NOTE: if you delete the default network,, compute engine, GKE and APP engine dont work.

**Now we create VPC**:

- Create a instance template with custom network, the create instance group with 4 instance: Success
- Increase the instance number to 5: Fail
- Expand the Subnet from /29 to /28: Success
- Verify that the VM creation success.

Refer: the image VM-creation-pre-subnet-expansion and VM-creation-post-subnet-expansion

> Note: VPC cant be delete if they are referred by some resources like instance template or group etc.

## Routes and firewall rules

### Routing tables

This section explain how GCP route traffic between different components.

By default every network has a route in  a network send traffic directly to each other between subnets.
Also a default route that directs packets to destinations that are outside the network.

Apart from the above routes we can create special custom routes, which may override the existing routes.

Defining routes do not guarantee that packet will be received by next hop. Firewall rules should also allow the traffic.

Default network have a pre-configured firewall rule which allows every component to communicate to each other.

Manually created network do not have any firewall rules and hence we should be defining them.

**Route match a packets by destination IP address**, however firewall rules are should also match for successful communication.

### Firewall rules

Firewall rules protect your VM instances from an unapproved connections both inbound an outbound.

VPC network function as a distributed firewall, hence firewall rules are applied to the network as a whole and not specific to instances.

But the rules are applied to allow or deny traffic at instance level.

Firewall rules are defined not only on the instance to communicate with external or other GCP networks, but also between instance on same network.

Firewall rules are stateful, this means that if communication between source and destination are allowed then all subsequent communication will be allowed. They are bidirectional once a session is established.

If all firewall rules are deleted, then by default *deny all ingress* and *allow all egress* is applied.

## How are route defined

Route contains the network IP(or CIDR) as well the network name. So when a request comes instance, it forwards the packet to desired network by consulting the routing tables.

## Creation of route

If there is no Network, no routes can exists. *In case you delete the default network.*

Route is created when a network is created. Also when a subnet is created. This enables VMs to communicate on the same network.

Routes in route collection can be configured to one or multiple instances.

Route applies to instance if network and instance tag is matched.

If the network tag matches and there are no instance tag, the the route is applied to all the instance in the network.

Then compute engine then creates individual read only routing tables for each of the instances.

## Creation of firewall rules

If there is no Network, no firewall rules can exists. *In case you delete the default network.*

Firewall rules consist of following parameters:

- **Direction** : ingress or egress (the rules are validated based on the flow of the traffic, for example: for egress traffic ingress rules are not validated.)
- **Source or destination** : source are configured in inbound rules to identify the host. Can be IP address, source tag or a svc account. Similarly, destination can be specified as part of the rule with one or more ranges of IP address.
- **Protocol or port** : rules can be restricted to apply to specific protocol only or combination of protocols and ports.
- **Action** : allow or deny
- **priority** : order in which rules are evaluated. First matching rules is applied
- **Rule assignment** : All rules are assigned to all instance in the network, but they are no applied.

**Examples**: stop undesired connection to external VM or network from your instances. and to prevent unauthorized connection to be received by the instance.

## Pricing

- Price are involved for each type of traffic type:
  - **ingress**: no charge for traffic. Resources receiving the traffic will be charged like VMs or LBs.
  - **Egress to same zone(internal IP)**: No charge
  - **Egress to google product**: No charge - you tube, Maps, drive
  - **Egress to different GCP services(same region)**: No charge
  - **Egress b/w zones in the same region**: $0.01 /GB
  - **Egress b/w same zone using external IP**: $0.01/GB
  - **Egress b/w region within US and Canada**: $0.01/GB
  - **Egress b/w regions not including traffic b/w US regions**: Varies
- Price for External IP address:
  - **Static IP address(not in use)**: $0.010/hour
  - **Static & ephemeral IPin standard VM**: $0.004/hour
  - **Static & ephemeral IP in preemptible VM**: $0.004/hour
  - **Static or ephemeral attached to forwarding rules**: No charges

> NOTE: the above are subject to change please use price calculator. For example: you can choose n1-standard-1 us-central1 with 100GB egress/monthly b/w US and EMEA.

## Network design pattern

### Increase availability on same region

With multiple zone **us-west-1a**, **us-west-1b** on same region with a single subnet. This may save from additional security complexity.

### Globalization

Need to create multiple subnet on different zones of different regions. Less failure across different failure domains. We can  use global HTTP load balancer to route traffic to the healthy region that are closer to the region. This also help lower latency and lower network cost for the project.

### Security

Whenever possible we can remove external IP address, and use cloud NAT.  **Cloud NAT** allow your application to communicate with internet or global network in controlled and efficient manner. This can be configure for update, patching and other required services of the cloud instances. Cloud NAT will allow internal traffic to reach out to internet but not from internet. In other words Cloud NAT provide internet access to VPC's private instances.

VPC routing using cloud internet gateway manages access to the Google APIs and other third party services on the internet. For example if we want to implement cloud store service in any on the VM we need to allow them per subnets. With **Google Private Access** enabled we can accesses internet without external IP address. Private Google Access is enabled at the subnet level. When it is enabled, instances in the subnet that only have private IP addresses can send traffic to Google APIs and services through the default route (0.0.0.0/0) with a next hop to the default internet gateway.

> NOTE: When instances do not have external IP addresses, they can only be reached by other instances on the network via a managed VPN gateway or via a Cloud IAP tunnel. Cloud IAP enables context-aware access to VMs via SSH and RDP without bastion hosts. For more information about this, see this blog post.

## Cloud NAT

Cloud NAT is a regional resource(if you have VM instances in multiple regions, you’ll need to create a NAT gateway for each region) and VPC network specific(if there are multiple VPC for a network you need create multiple cloud NAT for each VPC). *Hence, when we create cloud NAT, we provide the VPC(network) and the region*.

You can configure it to allow traffic from all ranges of all subnets in a region, from specific subnets in the region only, or from specific primary and secondary CIDR ranges only.

### Cloud NAT logging

Cloud NAT logging allows you to log NAT connections and errors. When Cloud NAT logging is enabled, one log entry can be generated for each of the following scenarios:

When a network connection using NAT is created.
When a packet is dropped because no port was available for NAT.
You can opt to log both kinds of events, or just one or the other. Created logs are sent to Cloud Logging.

## Cloud Router

Google Cloud Router dynamically exchanges routes between your Virtual Private Cloud (VPC) and on-premises networks by using Border Gateway Protocol (BGP)

## IAP

gcloud compute ssh vm-internal --zone us-central1-c --tunnel-through-iap
