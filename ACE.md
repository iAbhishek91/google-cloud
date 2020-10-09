# Associate Cloud Engineer Certification

## Scope

- deploy applications
- monitor applications
- manages enterprise solutions
- use of google cloud console.
- CLI interface to perform common platform-based tasks to maintain one or more deployed solutions that leverage manged or self managed services on GCP.

E2E (s)he should be:

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

## Study guide

Qwiklab: Google Cloud Fundamentals: Core Infrastructure
Qwiklab: Architecting with Google Cloud Platform: Infrastructure
Udemy: Google Cloud Platform (GCP) Fundamentals for Beginners(Janakiram MSV)
Udemy: Google Associate Cloud Engineer: Get Certified 2020 (Dan Sullivan)
Udemy: Linux Commands Line Basics(Ahmed Alkabary)

## Main modules and topics to know in depth

- *setting up a cloud solution env*
  - create projects (org >> folders >> projects >> resources) - DONE
  - manage users in cloud identity (manually and automated) - you need a domain to enable cloud identity.
  - enabling APIs within project - DONE
  - provision one or more stack driver workspace - DONE
  - Create one or more billing accounts - DONE
  - link project to a billing account - DONE
  - establishing billing account - DONE
  - setting up billing exports to estimate daily/monthly charges - DONE
- *Planning and configuring a cloud solution*
  - **planning and estimate GCP product use using price calculator** - DONE
  - **planning and configure compute resources**
    - select appropriate compute choice for a given workload (compute engine, GKE, App Engine flexible, Cloud Run, Cloud Functions)
    - Using preemptible VMs and custom machine types as appropriate. - DONE
  - **Planning and configuring data storage options**
    - cloud SQL, BigQuery, Cloud Spanner Cloud Bigtable) - DONE
    - Choose storage options (standards, nearline coldline archive) - DONE
  - **Planning and configuring network resources**
    - differentiating load balancing options - DONE
    - identifying resources options
    - configuring cloud DNS.
- *Deploying and implementing a cloud solution*
  - **Compute engine**
    - launch compute engine using cloud console, cloud SDK(gcloud), assign disk, availability policy and SSH keys. - DONE
    - create an auto-scaled managed instance group using an instance template. - DONE
    - Generating a custom SSH key for instances. - DONE
    - Configuring a VM for stackdriver monitoring and logging. - DONE
    - Accessing compute quotas and requesting increase. - DONE
    - Installing the stack driver agent for monitoring and logging. - DONE
  - **GKE**
    - Deploying k8s cluster -DONE
    - deploying a container appliction to GKE using pods - DONE
    - configure GKE application monitoring and logging - DONE
  - **App engine | Cloud Run | Cloud Function**
    - deploying and application, updating scaling configuration, version and traffic splitting.
    - Deploying an application that receives Google Cloud events (cloud pub/sub events, cloud storage obj change notification events)
  - **cloud SQL | Cloud datastore | BiqQuery | cloud spanner | cloud pub/sub | cloud big table | cloud Dataproc| cloud Dataflow| cloud Storage**
    - initialize data system with products.
    - Loading data from CLI, API transfer, import/export load data from cloud storage, streaming data to cloud pub/sub.
  - **cloud VPC | Cloud VPN | cloud load balancer**
    - create VPC with subnets - DONE
    - launching a compute engine instance with custom network configuration (eg internal-only IP address, Google private access, Static external and private IP address, network tags.) -  DONE
    - create VPN between a google VPC and an external network using cloud VPN. (VPN peering | interconnect | )
    - Creating a load balancer to distribute application network traffic to ana application
      - global http(s) load balancer
      - global SSL proxy load balancer
      - global TCP proxy load balancer
      - regional network load balancer
      - regional internal load balancer
  - **cloud marketplace**
    - browser cloud market place catalog and viewing solution details - DONE
    - deploying a cloud marketplace solution - DONE
  - **cloud deployment manager**
    - developing deployment manager templates
    - launching deployment manager templates
- *ensure successful operation of a cloud solution*
  - **Manage compute resource**
    - single VM instance - Start | Stop | Edit configuration or Delete an instance - DONE
    - SSH/RDP to the instance - DONE
    - Attaching a GPU to a new instance and installing CUDA libraries. - DONE
    - Viewing current running VM inventories - DONE
    - Working with snapshots - create snapshots, veiw snapshots | delete snapshots - DONE
    - Working with instane groups - set autoscaling parameters, assing instance template create an instance template , removing instance group. - DONE
    - Working with management interfaces - cloud console, cloud shell, Gcloud SDK. - DONE
  - **Managing Kubernetes Engine resources**
    - Viewing current running cluster inventory (nodes, pods services etc) - DONE
    - browsing the container image repository and viewing container image details
    - working with node pools - add, edit or remove a node pool - DONE
    - working with pods - add, edit or remove pods - DONE
    - working with services - add, edit or remove services. - DONE
    - working with stateful applications - persistent volumes, stateful sets - DONE
    - working with management interfaces - cloud console, cloud shell,cloud sdk - DONE
  - **Managing App Engine & cloud run resources**
    - Moving objects between cloud storage buckets - DONE
    - Converting cloud storage buckets between storage classes - DONE
    - setting object life cycle management policies for cloud storage buckets - DONE
    - executing queries to retrieve data from data instances (cloud SQL, BigQuery, cloud Spanner, cloud Datastore, cloud Bigtable) - DONE
    - Backing up and restoring data instances
    - Reviewing job status in cloud dataproc, cloud dataflow or big query - DONE
    -working with management interfaces (cloud console, cloud shell, cloud SDK) - DONE
- *Configuring access and security*
  - **IAM**
    - Assign user predefined IAM roles within a project - DONE
    - IAM role assignment
    - IAM role to accounts or Google group - DONE
    - Define custom IAM roles - DONE
    - manage service accounts - DONE
    - Assigning svc accounts to VM - DONE
    - granting access to svc account in another project - DONE
    - viewing audit logs for project and manged services - DONE

## Reference

[Google Cloud Platform Overview:](https://cloud.google.com/docs/overview/)
[Google Cloud Identity:](https://cloud.google.com/identity/)
[Google Cloud Pricing Calculator:](https://cloud.google.com/products/calculator/)
[Google Cloud Billing documentation:](https://cloud.google.com/billing/docs/)
[Cloud SDK installation and quick start:](https://cloud.google.com/sdk/#Quick_Start)
[gcloud tool guide:](https://cloud.google.com/sdk/gcloud/)
