# Persistent/Non-Persistent Disk

Below are the storage option used by VM - there are different type based on price and performance.

By default one single boot persistent disk is attached with each VM that contain the operating system. When application need more storage we need to choose one or more additional storage options for your instance.

Types are as below:

- **Zonal persistent disk**: Efficient | reliable block store | 10GB to 64TB | Max/VM: 257TB | encrypt at rest | Custom encrypt key |
- **Regional persistent disk** HA (replicated in 2 zones) | regional block store. | 10GB to 64TB | Max/VM: 257TB | encrypt at rest | Custom encrypt key |
- **Local SSD** High performance | transient | local block storage | 375GB | encrypt at rest | No custom encrypt key | limit of 24 local SSD partition (again based on machine type) for max of 9 TB per VM. | cannot be used as boot device | need to format and mount the device before using it.
- **Cloud storage buckets** Refer: STORAGE-0X-cloud-storage.md
- **FileStore** Refer: STORAGE-0X-Filestore.md

> NOTE: even though cloud-storage and filestore can be attached to VMs we are focusing on the block storage.

- block storage devices are similar to hard disk.
- They are independent of VMs and can be attached to the VMs as required. (Apart from local SSD, which are deleted when the VM is deleted)

> Independent means lifecycle of persistent disk are not dependent on VMs. Specifically Zonal an Regional persistent disk.

- Share single disk b/w multiple VMs, one VM can be the writer and others are reader.

> Due to this one disk can be attached to multiple VMs where one VM write and other may read.

- Both supports SSD(also known as balanced) and HDD(also known as standard).

## Format, Mount local SSD

- Any partition format (file system, ext1,2,3,4,xfs) and configuration are allowed.
- The mount and formatting of Local SSD is to be done once the VM is up and running.

```sh
# login to VM using SSH
# Identify the local SSD you want to mount, mostly they have standard names, sda(for SCSI mode) or nvme0n1(for NVMe mode)
lsblk # lists all block devices

# for the device(which will delete all the content and loads a new filesystem on the device.)

# for the disk with EXT4 fs
mkfs.ext4 -F /dev/SSD_NAME

# create a directory on which the device will be mounted
mount /dev/SSD_NAME /mnt/disks/MNT_DIR

# give access to the disk
chmod +w /mnt/disks/MT_DIR

# optionally you can mak a entry in /etc/fstab (very important if you want to mount the device automatically after restart)
# to find the UUID for the device, use blkid command
echo UUID=`sudo blkid -s UUID -o value /dev/disk/DEV_NAME`
```
