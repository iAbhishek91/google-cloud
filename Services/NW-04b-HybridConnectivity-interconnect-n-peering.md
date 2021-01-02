# Interconnects and peering services

There are different way to connect your network with GCP network.

- **VPN** refer NW-04a-Hybridconnectivity-VPN.md
- **Direct Peering** Connect N * 10G transport circuits for private cloud traffic to Google cloud at Google POPs.
- **Carrier peering**  are chosen if you are not near to the GCP network.

> Both dedicated and partner interconnect do not require internet as they are LAYER-2(data-link layer) service. LAYER-2 allows vLAN connection into Googles cloud and provides access to internal IP address(RFC 1918) of GCP.

- **Dedicated interconnect** Private (direct) connection between you and google for your hybrid cloud workloads.
- **Partner interconnect** Connection though the largest partner network of service providers. This option is chosen if customer are not near to GCP network.*do not requires internet*. Egress (outbound connectivity cost is lower, when we access cloud from on-premise)

> Both dedicated and partner peering requires internet as they are LAYER-3(network layer) service.

*refer* Refer NW-04b-type-of-interconnect-n-peering.png

## Interconnect

- Connects to On Premise networks to google cloud.
- Similar to VPN but with high bandwidth and low latency because of physical connection at LAYER-2.
- cost effective as we don't have by internet
- Very very high SLA 99.99%

- **Use cases**
  - efficient when huge amount of data.
  
- **Set up**
  - need to provision a cross connect between your network router and GCP in a *co-located facility*. *Refer: NW-04b-direct-interconnect.png*
  - To exchange the routes between the network, we *provision a BGP* between cloud router and on-premise router. This is true for partner interconnect as well. *Partner interconnect is just adds a extra hop in the between your router and cloud router*.

> NOTE: **Co-located facility** are geographic location defined by google where we can create dedicated interconnect. If you are not located near the co-located facility the consider **partner interconnect**. There are list of partners that are authorized and listed by Google who extends interconnect facility on behalf of google.

- **VLAN Attachment** (also known as interconnect attachment) describes which LAN can connect with on premise network through interconnect.

For Dedicated Interconnect, the VLAN attachment allocates a VLAN on an interconnect and associates that VLAN with the specified Cloud Router. It is possible to associate multiple, different VLAN attachments to the same Cloud Router.

When you create the VLAN attachment, specify a Cloud Router that's in the region containing the subnets that you want to reach. The VLAN attachment automatically allocates a VLAN ID and BGP peering IP addresses. Use that information to configure your on-premises router and establish a BGP session with Cloud Router.

## Peering

These services *Direct and Carrier peering* is required only if you require access google(G-suite, youtube, maps etc) & GCP properties.

In case of peering the connection is made between *your network and google's broad reaching edge network*. Routes are again shared using BGP between your network and BGP network.

There is no SLA.

POP *point of presence* are googles edge network *where googles network connects with rest of the internet* which are available on over 90 internet exchanges and 100 interconnect facilities.

Again if you are NOT near the *internet exchange* & *interconnect facilities* OR do not meet googles peering requirements then choose carrier peering.

## Use cases

- Running complex legacy database like SAP or mainframe or oracle on -premise which is hard to migrate to cloud, can remain on premise, however the modern application can run on cloud communicating with the on-premise database. these type of connections b/w cloud and on premise are performed by Interconnect.
