# gcloud

It is the primary CLI tools to create and manage Google Cloud resources.

gcloud CLI version is same as the SDK.

Few examples, create and manage:

- compute engine VM instance and other res
- cloud SQL instance
- GKE cluster
- cloud dataproc cluster and jobs
- cloud DNS managed zones and record sets
- cloud Deployment manager deployments

- deploy App engine application
- manage authentication
- customize local configuration

## Cheat sheet

[Cheat sheet](https://cloud.google.com/sdk/docs/cheatsheet)
[Practice](https://ssh.cloud.google.com/cloudshell/editor?page=editor&_ga=2.62336426.702647180.1599546622-709608325.1596613385&_gac=1.93400687.1596613385.CjwKCAjwsan5BRAOEiwALzomX4P0FSrVgDyfLlilFkWE5WIykwC79JXGYy8bzTet51qSl_pgH6_K5xoCtrYQAvD_BwE)

## Syntax

gcloud GROUP | COMMAND \[--account=ACCOUNT\] \[--billing-project=BILLING_PROJECT\] \[--configuration=CONFIGURATION\] \[--flags-file=YAML_FILE\] \[--flatten=[KEY,…\]\] \[--format=FORMAT\] \[--help\] \[--project=PROJECT_ID\] \[--quiet, -q\] \[--verbosity=VERBOSITY; default="warning"\] \[--version, -v\] \[-h\] \[--impersonate-service-account=SERVICE_ACCOUNT_EMAIL\] \[--log-http] \[--trace-token=TRACE_TOKEN\] \[--no-user-output-enabled\]

ref for all details: [gcloud docs](https://cloud.google.com/sdk/gcloud/reference)

## Help

--help provide detail help about the command
-h one line summery of the command

## Best practices

Gcloud command often require zone, region and projectID.

- keep this as environment variables
  - save the variables in a .sh file
  - include that as part of .profile file using source <file_name>.sh

## Properties

Properties are like parameter which governs the behavior of the gcloud CLI and other SDK.

Two way we can pass properties, using global or can be set using command flag using "-". Value of flag takes precedence.

## Configuration

Configuration is named set of properties. Default is a named configuration that is used by default.

```sh
# list all the config.
gcloud config list

# change the project
gcloud config set project [PROJECT_ID]
```

## Suppressing prompt

--quiet or -q

- Disable all interactive prompt
- In events of inputs is needed, defaults will be used. If there is no default err will be raised.
- Useful when scripting

## Suppressing writing to terminal

--no-user-output-enabled

- supressing printing command output to std output and std err.

## Logging

--verbosity

- adjust verbosity to appropriate level (debug, info, warning, error, critical or none)

## output format

The output is by default pretty printed to std output.

--format

- provide required format (json, csv, yaml, table, value, etc...)
- we can also use projections and filter.

## SSH

```sh
ssh -i ~/.ssh/google_compute_engine abhishekdas@34.105.144.159
connect with vs studio
ls
```

## Zone

```sh
#view zone you are currently and its status
gcloud compute zones list | grep us-central1

#set new default zones
gcloud config set compute/zone us-central1-c
```

## Auth

```sh
# gcloud command is performed by a logged in user(account)
# If the user do not have any permission to any resource the command will fail.
# However we can change the account that is being currently used to high privilege account.
gcloud auth activate-service-account --key file credentials.json

## validate the above change
gcloud config list

## to validate the list of all validated user in cloud shell. Note only one will be active at a time.
gcloud auth list

## to change the active account
gcloud config set account [username]
```

## VM / Network

```sh
# create a new VM in default zone
gcloud compute instances create "my-vm-2" \
--machine-type "n1-standard-1"
--image-project "debian-cloud"
--image "debian-9-stretch-v20170918"
--subnet "default"

## Validate the VM
gcloud compute instances list

## SSH in the VM
gcloud compute ssh instance-1 --zone asia-south1-a

# Copy files from cloud shell VM to another VM
gcloud compute scp index.html first-vm:index.nginx-debian.html --zone=us-central1-c

# list all the network and subnet
gcloud compute networks list
gcloud compute networks subnets list

# delete a network
gcloud compute networks subnets delete london --region=europe-west2
gcloud compute networks delete abhishek
```

## cloud SQL

```sh
# connect to sql instance
gcloud sql connect demo-db # enter the password to connect.
```

## IAM

```sh
# list all the user
gcloud auth list

# list only the services that are enabled
gcloud services list
gcloud services list --enabled

# list only the services those are available to project to enable
gcloud services list --available

# enable iam API
gcloud services enable iam.googleapis.com

# create service account
gcloud iam service-accounts create svc-ac-name \
--display-name "svc-ac-1" \
--description "svc account with editor role"

# view the list of policies assigned to the project (policies are binding between identity and roles)
gcloud projects get-iam-policy $GOOGLE_CLOUD_PROJECT
#- members:
#  - user:abhi.das2007das@gmail.com
#  role: roles/billing.projectManager
#- members:
#  - user:abhi.das2007das@gmail.com
#  role: roles/compute.admin
#- members:
#  - serviceAccount:service-911427390672@compute-system.iam.gserviceaccount.com
#  role: roles/compute.serviceAgent
#- members:
#  - serviceAccount:service-911427390672@container-engine-robot.iam.gserviceaccount.com
#  role: roles/container.serviceAgent
#- members:
#  - serviceAccount:911427390672-compute@developer.gserviceaccount.com
#  - serviceAccount:911427390672@cloudservices.gserviceaccount.com
#  - serviceAccount:service-911427390672@containerregistry.iam.gserviceaccount.com
#  role: roles/editor
#- members:
#  - user:abhi.das2007das@gmail.com
#  role: roles/owner
#- members:
#  - user:abhi.das2007das@gmail.com
#  role: roles/recommender.billingAccountCudAdmin

# grant the service account with project viewer role
gcloud projects add-iam-policy-binding $GOOGLE_CLOUD_PROJECT \
--member serviceAccount:svc-ac-name@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com \
--role roles/viewer
#- members:
#  - serviceAccount:my-svc-account@nice-beanbag-288720.iam.gserviceaccount.com
#  role: roles/viewer
```

## GKE and cloud registry

```sh
# Enable container API, when we do it from UI(cloud console) it is automatically enable when we open kubernetes engine.
gcloud services enable containerregistry.googleapis.com

# pull from docker hub
docker pull busybox

# Create a new image from the docker file
docker build .-t mybusybox
docker tag mybusybox gcr.io/$PROJECT_ID/mybusybox:latest
docker run gcr.io/$PROJECT_ID/mybusybox:latest

# upload in google container registry
gloud auth configure-docker
docker push gcr.io/$PROJECT_ID/mybusybox:latest

# create a cluster called k1
gcloud container clusters create "k1"

# launch a kubernetes cluster on a specific zone and number of nodes
gcloud container clusters create "k1" --zone $MY_ZONE --num-nodes 2

# Check the version of kubernetes
k version

# View the nodes on compute engine that are span for the k8s cluster.
```

```sh
# create a node pool with all possible options available
# default machine type: e2-medium
# default num-nodes: 3
# get the valid image type(specific to a location): "gcloud container get-server-config --region us-central1"
# refer min-cpu-platform notes on GKE.md file, find min-cpu-platform availability gcloud compute zones describe ZONE_NAME
# disk-type is pd-standard o=OR pd-ssd
# disk-size is 10GB
# max-surge-upgrade is no of extra nodes to be created on each upgrade of the node pool
# service account that are will be part of the VM
gcloud container node-pools create my-pool \
--cluster gke-k8s-cluster \
--zone europe-west1-c \
--machine-type e2-small \
--num-nodes 1
--image-type COS
--min-cpu-platform "Intel Cascade Lake"
--node-locations=[ZONE1, ZONE2]\
--disk-type=pd-standard
--disk-size=10GB
--max-pod-per-node=50
--max-surge-upgrade=1
--preemptible
--max-nodes=18
--max-nodes=12
--service-account=svc-acc
--node-taints=key1=val1:NoSchedule, key2=value2:NoExecute
--node-labels=label1=value1,label2=value2
# view all the node-pools on a cluster
gcloud container node-pools list --cluster cluster cluster-name

# to view the details of a specific node-pools
gcloud container node-pools describe pool-name --cluster cluster-name

# resizing a node-pool, if only default node-pool is there, then omit --node-pool
gcloud container clusters resize cluster-name --node-pool pool-name --num-nodes 2

# upgrading node pool to same version as master
gcloud container clusters upgrade cluster-name
# upgrading node pool to specific version
gcloud container clusters upgrade cluster-name --node-pool pool-name

# deploy a pod to a specific node-pool (in pod yaml)
nodeSelector:
  cloud.google.com/gke-nodepool: nodepool-name

# deleting a node pool
gcloud container node-pools delete pool-name --cluster cluster-name
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
