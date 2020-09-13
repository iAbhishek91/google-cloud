# Compute Engine (IaaS)

- Its infrastructure as a service offering of GCP.

## Features

from Console or GCloud command line tool.

- choose a **machine type**(based on power consumption) - how much memory and CPU we can need. Option of creating custom VM are also available.
- **GPU** offers processing power, choose if required. These are mainly required for ML and data processing.
- **Persistent Storage** is also required, we can choose between standards(default) and ssd.
- **Local SSD** are not permanent, as they are deleted when VMs terminate.
- select the **boot image** of the OS - windows and linux, also import images from other places.
- we can also pass a **startup scripts**, to be executed when a VM boots to configure their VMs.
- Take **snapshots of the VMs** when we need to migrate to another region.
- Auto scaling.
- **host maintenance** regular maintenance activity will migrate your VMs to other physical server without downtime.

## Instance template

- Use instance template to create VMs instance based on pre-existing configuration.
- This also help you to create VMs with identical configurations.
- AFter instance template is created its not possible to update it, as its make sure that VM types are identical.
- Instance templates are global resource. But it points to many resources that are specific to a region and zone. for example persistent disk. hence to create a instance from instance template make sure the resources defined in the template is available on the same region or zone.
- Labels defined on instance template are not applied on the template but on the VM instance those are created from the template.

## Regular VMs

Dedicated VMs, it will not be terminated if its required else where.

## what are preemptible VMs

- These VMs can be taken away anytime if they are required anywhere else.
- its a good way to save money, as they are cheaper.
- **use cases**: VMs which mainly use to run long jobs with no human interactions. Make sure to start and stop the job in case of failure. Basically jobs running of preemptible VMs are to be fault tolerant.
- It last only 24 hours, or sooner.
- Automatic restart is not possible on preemptible VMs.
- Preemptible instance cant live migrate to regular VMs.
- your application has 30 seconds to exit gracefully.
- Using preemptible Vms with instance group will bring back the VM automatically when its preempt.

## Instance Group

- Create a managed instance group using template. This will create a VM which will be managed.
- Managed instance group help you in auto scaling.

There are two type of instance group: managed and un managed.

### Managed Instance Group (MIG)

- They are group of VMs that are identical in nature.
- **Use cases** are operate on multiple identical VMs.
- They offer, HA(Auto healing, Regional and load balancing), auto scaling and auto updating.
- MIGs can be classified again in regional(evenly distributed over multiple zones in a specific region) and zonal(in a single zone). Hence regional MIG are HA and recommended by Google.
- Each MIG can have only 2000 VMs.
- MIGs can be again classified as stateful and stateless
  - Only stateless MIG supports auto scaling.
  - Stateful MIG supports preserving state of disks and metadata.

### UnManaged Instance Group

- Are group of VMs that are not necessarily identical(as they don't share a common instance template).
- **Use Case** mostly used to accommodate pre-existing task and load balanced b/w them.
- only load balancing feature is available. *FEATURES UNAVAILABLE: HA(Auto healing, Regional), auto scaling and auto updating*

## Autoscaling

Autoscaling is supported for stateless MIG only.

- Three mode of auto scaling
  - Auto scale (scale up and down)
  - Dont autoscale
  - Auto scale only up

- Three matrices which supports autoscaling
  - CPU utilization (based on percentage)
  - HTTP load balancing (based on percentage)
  - Stackdriver monitoring metrics (many combinations)

- Scale in controls
  - % of scaling or by absolute numbers of VMs
  - over a time period

- recommended settings
  - minimum 3 zone
  - with max number of instance greater than or equal to number of zone.

## Auto healing

We need to create health check, else it will enable autoHealing based on VMs status (stopped). Google recommends to define health check for auto-healing.

[auto healing instance in migs](https://cloud.google.com/compute/docs/instance-groups/autohealing-instances-in-migs)

## Auto restart

Its a simple feature, if VM stops due to  non-user initiated activity, the compute engine will start backup.

Think if you need backup of the application.

is your application idempotent or stateless, choose the option based on this factors.

## Sole tenant nodes

- deploy your VM on a dedicated machine.
- No other project share the machine.
- Feature are same as in multi tenant node, but it comes with a added layer of hardware isolation.
- one to one mapping between the nodes and the physical server. We can have multiple VMs create on the physical server for the same project.
- Sole tenancy is may be a temporary requirement, if that case we can change the VM tenancy as necessary.
- configurable maintenance policy - sole tenant nodes let you control the behavior of the host during maintenance.
- *We can discuss later about node-template, node-group,node-type,node-affinity and anti affinity*
- **User cases**
  - Finance and health care project may required extra security feature for meeting their compliance.
  - Special workload like gaming app may require.
  - Windows VMs which comes with licencing based on physical server, per core, per processor.

## Charge

- Charged in seconds for minimum of 1 minutes.
- **Sustained use discount** offered if VMs are running for a significant portion of the billing month.
- **Committed use discount** offered if procurement is based on 1 year or 3 year contract.

## SSH

There are two way we can manage SSH key for a VM if we want. Else GCP manages few keys already.

- **specific for each VM** In Instance template or instance under security you can place the public key and later we can use the private key.

```sh
ssh -i ~/.ssh/id_rsa abhishek.das1@34.72.187.35
```

- **specific for all VM** In compute engine we can manage under metadata

> NOTE: Alternatively we can have OS login, where we don't need to manage SSH keys.

## Lifecycle of a VM

**PROVISIONING**: Resource are being allocated for the instance. And moves to staging stage.
**STAGING**: Resource have been acquired and the instance is being prepared for first boot. And moved to running.
**RUNNING**: Either its booting up or running.
**STOPPING**: Stop can be requested by user or due to failure. This will temporary status and instance will move to terminated. *Use cases: need the VM in future for internal IP, MAC or Storage | need to change some OS level property which need restart*
**REPAIRING**: happens because the instance encountered an internal error or the underlying machine is unavailable due to maintenance. During this time underlying machine is unavailable for maintenance. If repair is successful, the machine is moved to Running state.
**TERMINATED**: VM is shutdown.
**SUSPENDING**: the instance is being suspended manually. Its like sleep. *Use cases: currently not required, but can bring back the instance quickly | you dont mind paying google to preserver the state of ur VM.*.
**SUSPENDED**: instance is already suspended, resume it or delete it.

> PRICING for suspended: Preserver the state(state of RAM) of the VMy for u. pay for resource that are still attached to the VM (disk, internal ip, MAC address), ephemeral ext IP address are released. But no cost of running the VM.
> PRICING for terminated: no charge for running the instance, the state of the VM is not preserved. you pay for resource that are still attached to the VM (disk, internal ip, MAC address), ephemeral ext IP address are released. But no cost of running the VM.

[VM lifecycle](https://cloud.google.com/compute/docs/instances/instance-life-cycle)

## Installing Stack Driver agent

[Refer Stack driver docs.]((https://cloud.google.com/monitoring/agent/installation?_ga=2.259618700.-709608325.1596613385&_gac=1.83054052.1596613385.CjwKCAjwsan5BRAOEiwALzomX4P0FSrVgDyfLlilFkWE5WIykwC79JXGYy8bzTet51qSl_pgH6_K5xoCtrYQAvD_BwE#agent-install-debian-ubuntu))

## host maintenance

There are two option you have while server is going through maintenance: **first**: we can terminate the VM, **second**: we can move the VM to other server. (the second option is recommended by Google for un-interrupted service)

## External IP

- external IP are removed when VM are stopped or suspended.
- external IP link will be disabled in cloud console when firewall is disabled for HTTP & HTTPS.

## Quotas and request for increase

[GCP docs](https://cloud.google.com/compute/quotas)

```sh
# provide lists of project level quotas
## the below command do not list per region quota
gcloud compute project-info describe --project myproject

# to know per region quota
gcloud compute regions describe <region-name>
```

To request to increase the quotas in cloud console is free. If the quota increase and if you utilize the usage will be more.

Serviceusage.quotas.update permission is required, this already included in owner, editor and quota admin.

## Attributes required for VM pricing

### Instance

- Number of instance
- OS
- Machine Class
- Machine Family
- Series
- Machine type
- local SSD
- location
- ephemeral IP
- static IP
- avg running hours
- avg number of days in a week

### Self tenant nodes

- Since we are paying for the physical server (vCPU and memory) we need to pay extra for VMs on the sole tenant nodes.

### Persistent Disk

refer STORAGE-0X-Persistent-disk.md

### Cloud TPUs
