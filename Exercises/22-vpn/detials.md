# VPN connectivity

## Create 2 VPC, Firewall rules and VM instances

- Step-1:
  - should have two VPC network with one subnet.
  - First subnet
    - name: vpn-network-1
    - region: US-Central1
    - CIDR: 10.4.5.0/24
  - Second subnet:
    - name: vpn-network-2
    - region: Europe-west1
    - CIDR: 10.1.3.0/24
- Step-2:
  - two firewall rules are created for both the subnet
    - Allow ingress SSH and ICMP from all source.
- Step-3:
  - two VM, each on each subnet. hence they cant connect without VPC peering or shared VPC or VPN.
  - Validate communication:
    - Using internal IP address: not possible as they are not on same network
    - Using external IP address: possible as the communication occurs via internet.

## Create VPN gateway and tunnel

- Step-1:
  - Reserve two IP address:
    - Navigate to VPC >> External IP >> Reserve static address
    - First IP:
      - name: vpn-1-static-ip
      - region: us-central1
      - type: IPV4
    - Second IP:
      - name: vpn-2-static-ip
      - region: europe-west1
      - type: IPV4
- Step-2:
  - Create VPN gateways and tunnel
    - Navigate to hybrid connection >>  VPN
    - First VPN gateway
      - type: Classic VPN
      - name: vpn-1
      - network: vpn-network-1
      - region: us-central1
      - ip-address: vpn-1-static-ip (drop down)
    - First Tunnel
      - name: tunnel1to2
      - ip-address: vpn-2-static-ip (type)
      - IP pre-shared keys: gcprocks
      - routing option: route based
      - CIDR: 10.1.3.0/24 (this is the CIDR of the second subnet)
    - First VPN
      - type: Classic VPN
      - name: vpn-2
      - network: vpn-network-2
      - region: europe-west1
      - ip-address: vpn-2-static-ip
    - First Tunnel
      - name: tunnel2to1
      - ip-address: vpn-1-static-ip (type)
      - IP pre-shared keys: gcprocks
      - routing option: route based
      - CIDR: 10.5.4.0/24 (this is the CIDR of the first subnet)

Below are CLI generated for the above steps

```sh
gcloud compute --project "doctord-gcp-00-1862e0694142" target-vpn-gateways create "vpn-1" --region "us-central1" --network "vpn-network-1"

gcloud compute --project "doctord-gcp-00-1862e0694142" forwarding-rules create "vpn-1-rule-esp" --region "us-central1" --address "34.122.105.126" --ip-protocol "ESP" --target-vpn-gateway "vpn-1"

gcloud compute --project "doctord-gcp-00-1862e0694142" forwarding-rules create "vpn-1-rule-udp500" --region "us-central1" --address "34.122.105.126" --ip-protocol "UDP" --ports "500" --target-vpn-gateway "vpn-1"

gcloud compute --project "doctord-gcp-00-1862e0694142" forwarding-rules create "vpn-1-rule-udp4500" --region "us-central1" --address "34.122.105.126" --ip-protocol "UDP" --ports "4500" --target-vpn-gateway "vpn-1"

gcloud compute --project "doctord-gcp-00-1862e0694142" vpn-tunnels create "tunnel1to2" --region "us-central1" --peer-address "34.76.6.216" --shared-secret "gcprocks" --ike-version "2" --local-traffic-selector "0.0.0.0/0" --target-vpn-gateway "vpn-1"

gcloud compute --project "doctord-gcp-00-1862e0694142" routes create "tunnel1to2-route-1" --network "vpn-network-1" --next-hop-vpn-tunnel "tunnel1to2" --next-hop-vpn-tunnel-region "us-central1" --destination-range "10.1.3.0/24"
```

## Validate the setup

Wait for VPN tunnel status as established.

- Step-1:
  - two VM, each on each subnet. VPN is established.
  - Validate communication:
    - Using internal IP address: possible as they are not on same network, but VPN is established.
    - Using external IP address: possible as the communication occurs via internet.
- Step-2:
  - Remove external IP(by editing the VM) and test step-1 for internal IP only
  - It should b successful.
