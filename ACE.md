# Associate Cloud Engineer Certification

## Scope

- deploy applications
- monitor applications
- manages enterprise solutions
- use of google cloud console.
- CLI interface to perform common platform-based tasks to maintain one or more deployed solutions that leverage manged or self managed services on GCP.

E2S (s)he should be:

- Set up cloud solution environment
- Plan and configure a cloud solution
- Deploy and implement a cloud solution
- Ensure successful operation of a cloud solution
- Configure access & security

## Duration

2 hrs

## Pre-requisite

none

## One page official docs

[Docs](https://cloud.google.com/certification/cloud-engineer)

## Main modules and topics to know in depth

- *setting up a cloud solution env*
  - create projects (org >> folders >> projects >> resources)
  - manage users in cloud identity (manually and automated)
  - enabling APIs within project
  - provision one or more stack driver workspace
  - Create one or more billing accounts.
  - link project to a billing account
  - establishing billing account
  - setting up billing exports to estimate daily/monthly charges.
- *Planning and configuring a cloud solution*
  - **planning and estimate GCP product use using price calculator**
  - **planning and configure compute resources**
    - select appropriate compute choice for a given workload (compute engine, GKE, App Engine flxible, Cloud Run, Cloud Functions)
    - Using preemptible VMs and custom machine types as appropriate.
  - **Planning and configuring data storage options**
    - cloud SQL, BigQuery, Cloud Spanner Cloud Bigtable)
    - Choose storage options (standards, nearline coldline archive)
  - **Planning and configuring network resources**
    - differentiating load balancing options
    - identifying resources options
    - configuring cloud DNS.
- *Deploying and implementing a cloud solution*
  - **Compute engine**
    - launch compute engine using cloud console, cloud SDK(gcloud), assign disk, availability policy and SSH keys.
    - create an auto-scaled managed instance group using an instance template.
    - Generating a custom SSH key for instances.
    - Configuring a VM for stackdriver monitoring and logging.
    - Accessing compute quotas and requesting increase.
    - Installing the stack driver agent for monitoring and logging.
  - **GKE**
    - Deploying k8s cluster.
    - deploying a container appliction to GKE using pods.
    - configure GKE application monitoring and logging
  - **App engine | Cloud Run | Cloud Function**
    - deploying and application, updating scaling configuration, version and traffic splitting.
    - Deploying an application that receives Google Cloud events (cloud pub/sub events, cloud storage obj change notification events)
  - **cloud SQL | Cloud datastore | BiqQuery | cloud spanner | cloud pub/sub | cloud big table | cloud Dataproc| cloud Dataflow| cloud Storage**
    - initialize data system with products.
    - Loading data from CLI, API transfer, import/export load data from cloud storage, streaming data to cloud pub/sub.
  - **cloud VPC | Cloud VPN | cloud load balancer**
    - create VPC with subnets
    - launching a compute engine instance with custom network configuration (eg internal-only IP address, Google private access, Static external and private IP address, network tags.)
    - create VPN between a googld VPC and an external network using cloud VPN.
    - Creating a load balancer to distribute application network traffic to ana application
      - global http(s) load balancer
      - global SSL proxy load balancer
      - global TCP proxy load balancer
      - regional network load balancer
      - regional internal load balancer
  - **cloud marketplace**
    - browser cloud market place catalog and viewing solution details
    - deploying a cloud marketplace solution
  - **cloud deployment manager**
    - developing deployment manager templates
    - launching deployment manager templates
- *ensure successful operation of a cloud solution*
  - **Manage compute resource**
    - single VM instance - Start | Stop | Edit configuration or Delete an instance
    - SSH/RDP to the instance
    - Attaching a GPU to a new instance and installing CUDA libraries.
    - Viewing currect running VM inventories
    - Working with snapshots - create snapshots, veiw snapshots | delete snapshots
    - Working with instane groups - set autoscaling parameters, assing instance template create an instance template , removing instance group.
    - Working with management interfaces - cloud console, cloud shell, Gcloud SDK.
  - **Managing Kubernetes Engine resources**
    - Viewing current running cluster inventory (nodes, pods services etc)
    - browsing the container image repository and viewing container image details
    - working with node pools - add, edit or remove a node pool
    - working with pods - add, edit or remove pods
    - working with services - add, edit or remove services.
    - working with stateful applications - persistent volumes, stateful sets
    - working with management interfaces - cloud console, cloud shell,cloud sdk
  - **Managing App Engine & cloud run resources**
    - Moving objects between cloud storage buckets
    - Converting cloud storage buckets between storage classes
    - setting object life cycle management policies for cloud storage buckets
    - executing queries to retrieve data from data instances (cloud SQL, BigQuery, cloud Spanner, cloud Datastore, cloud Bigtable)
    - Backing up and restoring data instances
    - Reviewing job status in cloud dataproc, cloud dataflow or big query
    -working with management interfaces (cloud console, cloud shell, cloud SDK)
- *Access and security*
  - **IAM**
    - Assign user predefined IAM roles within a project
    - IAM role assignment
    - IAM role to accounts or Google group
    - Define custom IAM roles
    - manage service accounts
    - Assigning svc accounts to VM
    - granting access to svc account in another project
    - viewing audit logs for project and manged services
