# Configure NAT communication

- Create a VM without external IP, configure a NAT for the same network.
- Validate VMs can communicate with internet.
- Delete the NAT
- Validate the communication between VMs and Network.

## Steps

- Its simple creating VM, select the correct network for which you want to create a NAT. Also for proper validation dont select external IP for the VMs.
- Create a NAT for the same network, and location.
  - Name: doctord-nat
  - VPC network: abhi-vpc-gke
  - Region: europe-west2
  - Cloud router: doctord-router
  - NAT mapping
    - source(internal): only primary IP ranges.
    - NAT IP address: Automatic
    - Destination(read only): Internet

> Need to create a cloud router if not already available.