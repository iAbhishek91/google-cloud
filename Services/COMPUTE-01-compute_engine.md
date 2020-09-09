# Compute Engine (IaaS)

- Its infrastructure as a service offering of GCP.

## Features

from Console or GCloud command line tool.

- choose a machine type (based on power consumption) - how much memory and CPU we can need. Option of creating custom VM are also available.
- Storage is also required, we can choose between standards and ssd. Local SSD are not permanent, as they are deleted when VMs terminate.
- select the boot image of the OS - windows and linux, also import images from other places.
- we can also pass a startup scripts, to be executed when a VM boots to configure their VMs.
- Take snapshots of the VMs when we need to migrate to another region.
- Auto scaling.

## Normal VMs

Dedicated VMs, it will not be terminated if its required else where.

## what are preemptible VMs

- These VMs can be taken away anytime if they are required anywhere else.
- its a good way to same money, as they are cheaper.
- **use cases**: VMs which mainly use to run long jobs with no human interactions. Make sure to start and stop the job in case of failure.

## Charge

- Charged in seconds for minimum of 1 minutes.
- **Sustained use discount** offered if VMs are running for a significant portion of the billing month.
- **Committed use discount** offered if procurement is based on 1 year or 3 year contract.

## Attributes required for VM

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

## Self tenant nodes

## Persistent Disk

## Cloud TPUs
