# Hybrid Connectivity

## VPN

- **VPN** in general virtual private network allows two computer to communicate securely.
- it **encrypts** the data packets and also does **threat detection**.
- VPN in a way is a **CLIENT-SERVER** technology, where VPN gateway act as server and the VPN client as a client. *Due this reason for connecting two network using VPN we need TWO tunnel one for each client server communication*.

- connect On premises networks to google cloud VPC.
- **Managed Cloud VPN supports**:
  - *site to site* VPN connectivity
  - *static routes*: connection between VPN gateways & *dynamic routes*: connection between cloud router and vpn gateway.
  - *ikev1 and ikev2 ciphers*
- SLA of 99.9%
- its ideal for *low volume data* connection.
- It uses **IPSec** secure network protocol suite for data communication. This protocol ensures authentication and encryption of data packets. *Encryption is done by one VPN gateway and is decrypted by the other end*.

> cloud VPN do not supports dial in VPN connection using client VPN software.

## Two type of VPN

**HA VPN** : Supports Dynamic routing | HA within region with SLA of 99.9%

**Classic VPN** : Supports static and dynamic routing | No HA

## Connectivity step by step

> NOTE: here we are describing VPN topology mentioned in the VPN-topology.png.

- **STEP-1**: *Cloud VPN gateway* is a regional resource and connects to external internet using regional external IP addresses.
- **STEP-2**: *On-premise VPN gateway* can be a physical device on on premise or a software or hardware based device from other cloud providers.
  - Whatever may be the case, the gateway has a external IP address associated.
- **STEP-3**: *VPN tunnel* then connects both the external IP, which implements IPSec protocol suite and act as virtual medium for data communication.
- **STEP-4**: *Pair of VPN tunnel* MUST be established one for each network to communicate with other. *This is to do with the client server analogy of VPN. When private network wants to communicate with google VPC one VPN tunnel is used, and when Google VPC want to communicate with on-premise another VPN tunnel is used*.
  - Only when both the connection is established, the communication can happen.
- **STEP-5**: *MTU - maximum transmission unit: is the largest packet or frame size that can be sent over the network* of on-premise network must not be more than 1460 bytes.

## Dynamic routes in cloud VPN

Dynamic routes helps us to automatically propagate network configuration changes.

It will be difficult if we have growing network *we keep on creating subnet in the VPC*, the routes between the VPC and VPN should be configured manually.

To enable dynamic routing, both the VPN gateway must support BGP.

- We need to configure *could routers*.
  - Cloud routers uses *BGP: border gateway protocol*. *BGP: decides the routes dynamically by looking at all the routes available for the packet, between both the gateways and decides the suitable one to use.* Hence this allows traffic to flow for newly created subnet.
- For BGP: *another pair IP address* are required at each end of the VPN tunnel, these IP address should be of type link local. *with range in 169.254.0.0/16, this IP must not be part of any of the network and exclusively used for creating BGP session.*

> Link local IP addresses are address that are valid only for communication between the network segment and broadcast domain.
