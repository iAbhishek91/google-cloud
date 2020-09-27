# HTTPS load balancing between VMs

- Create two VM in two different zone.
- Create a node microservice to send the hostname
- Create a HTTP load balancer to point to both the VMs

## Steps

>NOTE: individual VM cant be used with LV, need to create a instance template and instance group

- Create two preemptive VM. *first vm | second vm*
  - Name: first-vm | second-vm
  - Region: europe-west2
  - Zone: europe-west2-a | europe-west2-b
  - Series: N1
  - Machine type: F1-micro
  - Debian GNU/Linux 10
  - Allow HTTP traffic
  - below startup script
  - preemptive vm
  - create health check (in instance group): http at port 1122
  - keep every thing else as default
  
```sh
# Startup script
curl -sSO https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh
sudo bash add-monitoring-agent-repo.sh
sudo apt-get update
sudo apt-get install stackdriver-agent
sudo service stackdriver-agent start
sudo service stackdriver-agent status
sudo apt-get install nodejs npm git -y
sudo apt-get update -y
sudo npm i -g -y yarn
```

- Clone a repo from my personal git hub

```sh
git clone https://github.com/iAbhishek91/display-hostname.git
cd display-hostname
yarn
node server.js
```

- Access the site using:
  - http://ext-ip-of-first-vm:1122
  - http://ext-ip-of-second-vm:1122

>NOTE: need to open firewall for the subnet.

- Configure load balancer
  - http load balancer (layer 7 load balancer)
  - internet to VMs (internet facing load balancer.)
  - Frontend:
    - IP ephemeral
    - port 80
  - backend:
    - instance group created
    - health check
