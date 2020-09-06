# Interconnects

There are different way to connect your network with GCP network.

- **VPN** multi GBPS VPN to securely connect private network or other cloud network with GCP. Cheeper compared to others.
- **Direct Peering** Private connection between you and google for your hybrid cloud workloads. *do not requires internet*
- **Carrier peering** Connection though the largest partner network of service providers. This option is choosen if customer are not near to GCP network.*do not requires internet*. Egress (outbound connectivity cost is lower, when we access cloud from on-premise)
- **Dedicated interconntect** Connect N * 10G transport circuits for private cloud traffic to Google cloud at Google POPs.

## Use cases

- Running complex legacy database like SAP or mainframe or oracle on -premise which is hard to migrate to cloud, can remain on premise, however the modern application can run on cloud communicating with the on-premise database. these type of connections b/w cloud and on premise are performed by Interconnect.
