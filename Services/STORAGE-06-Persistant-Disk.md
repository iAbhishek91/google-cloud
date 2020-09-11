# Persistent Disk

These disks are used by VM - there are different type based on price and performance.

Types are as below:

- **Zonal persistent disk**
- **Regional persistent disk**
- **Local SSD**
- **Cloud storage buckets**
- **FileStore**

- block storage device similar to hard disk.
- They are independent of VMs and can be attached to the VMs as required.

> Independent means lifecycle of persistent disk are not dependent on VMs.

- 64TB in Size.
- Can have one writer and multiple reader.

> Due to this one disk can be attached to multiple VMs where one VM write and other may read.

- Both supports SSD and HDD.
