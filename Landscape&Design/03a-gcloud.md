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
