# Deployment manager

- deploy a new VPC
- deploy a new firewall rule
- deploy VM

Step-1: Verify deployment manager API is enabled
Step-2: Navigate to cloud shell
Step-3: Create a folder and save create everything there.
Step-4: Navigate to editor from the cloud shell
Step-5: Create a config.yaml file

```yaml
# file config.yaml
resources:
# Create the auto-mode network
- name: mynetwork
  type: compute.v1.network # gcloud deployment-manager types list | grep network
  properties:
    autoCreateSubnetworks: true

# Create the firewall rule
- name: mynetwork-allow-http-ssh-rdp-icmp
  type: compute.v1.firewall # gcloud deployment-manager types list | grep firewall
  properties:
    network: $(ref.mynetwork.selfLink)
    sourceRanges: ["0.0.0.0/0"]
    allowed:
    - IPProtocol: TCP
      ports: [22, 80, 3389]
    - IPProtocol: ICMP
```

Step-6: Create template instance-template.jinja

```yaml
# file: instance-template.jinja
resources:
- name: {{ env["name"] }}
  type: compute.v1.instance  # gcloud deployment-manager types list | grep instance
  properties:
     machineType: zones/{{ properties["zone"] }}/machineTypes/{{ properties["machineType"] }}
     zone: {{ properties["zone"] }}
     networkInterfaces:
      - network: {{ properties["network"] }}
        subnetwork: {{ properties["subnetwork"] }}
        accessConfigs:
        - name: External NAT
          type: ONE_TO_ONE_NAT
     disks:
      - deviceName: {{ env["name"] }}
        type: PERSISTENT
        boot: true
        autoDelete: true
        initializeParams:
          sourceImage: https://www.googleapis.com/compute/v1/projects/debian-cloud/global/images/family/debian-9
```

Step-7: import the template in the config.yaml

modified config.yaml

```yaml
imports:
- path: instance-template.jinja

resources:
# Create the auto-mode network
- name: mynetwork
  type: compute.v1.network
  properties:
    autoCreateSubnetworks: true

# Create the firewall rule
- name: mynetwork-allow-http-ssh-rdp-icmp
  type: compute.v1.firewall
  properties:
    network: $(ref.mynetwork.selfLink)
    sourceRanges: ["0.0.0.0/0"]
    allowed:
    - IPProtocol: TCP
      ports: [22, 80, 3389]
    - IPProtocol: ICMP

# Create the mynet-us-vm instance
- name: mynet-us-vm
  type: instance-template.jinja
  properties:
    zone: us-central1-a
    machineType: n1-standard-1
    network: $(ref.mynetwork.selfLink)
    subnetwork: regions/us-central1/subnetworks/mynetwork

# Create the mynet-eu-vm instance
- name: mynet-eu-vm
  type: instance-template.jinja
  properties:
    zone: europe-west1-d
    machineType: n1-standard-1
    network: $(ref.mynetwork.selfLink)  
    subnetwork: regions/europe-west1/subnetworks/mynetwork
```

Step-8: deploy the config

```sh
# preview is like dry run, deployment manger will start creating the resource, but abort it before actually creating it.
gcloud deployment-manager deployments create dminfra --config=config.yaml --preview

# to actually creating a deployment.
gcloud deployment-manager deployments update dminfra
```
