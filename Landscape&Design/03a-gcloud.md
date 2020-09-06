# gcloud

## Zone

```sh
#view zone you are currently and its status
gcloud compute zones list | grep us-central1

#set new default zones
gcloud config set compute/zone us-central1-c
```

## VM

```sh
# create a new VM in default zone
gcloud compute instances create "my-vm-2" \
--machine-type "n1-standard-1"
--image-project "debian-cloud"
--image "debian-9-stretch-v20170918"
--subnet "default"
```

## GKE

```sh
# create a cluster called k1
gcloud container clusters create "k1"

# launch a kubernetes cluster on a specific zone and number of nodes
gcloud container clusters create "k1" --zone $MY_ZONE --num-nodes 2

# Check the version of kubernetes
k version

# View the nodes on compute engine that are span for the k8s cluster.
```

## Deployment manager

```sh
export MY_ZONE=us-central1-f

# see your project id
echo $DEVSHELL_PROJECT_ID

# create deployment template
resources:
- name: my-vm
  type: compute.v1.instance
  properties:
    zone: ZONE
    machineType: zones/ZONE/machineTypes/n1-standard-1
    metadata:
      items:
      - key: startup-script
        values: "apt-get update; apt-get install nginx-light -y"
    disks:
    - deviceName: boot
      type: PERSISTENT
      boot: true
      autoDelete: true
      initializeParams:
        sourceImage: https://www.googleapos.com/compute/v1/projects/debian-cloud/global/image/debian-9-streach-v20279$
    networkInterfaces:
    - network: https://www.googleapos.com/compute/v1/projects/PROJECT_ID/global/networks/default
      accessConfigs:
      - name: External NAT
        type: ONE_TO_ONE_NAT

# replace the ZONE with our zone and project id
sed -i -e 's/PROJECT_ID/'$DEVSHELL_PROJECT_ID template.yaml
sed -i -e 's/ZONE/'$MY_ZONE template.yaml

# build a deployment from the above template
gcloud deployment-manager deployments create my-first-depl --config template.yaml

# validate the status of the deployment just done
gcloud deployment-manager deployments list

# update the deployment, the above the template change.
gcloud deployment-manager deployments update my-first-depl --config template.yaml

# put arbitary load on VMs
dd if=/dev/urandom | gzip -9 >> /dev/null &
```
