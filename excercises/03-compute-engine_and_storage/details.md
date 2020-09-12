# Work with different storage options with cloud compute engine

## tasks

1. create a instance with local SSD, configure stackdriver agent and enable monitoring, configure the local SSD, save few data, take a snapshot, validate the disk attached - boot device and local device, suspends the VM and analyse the disk, stop the VM and analyze the disk and load the snapshot and analyze the disk, stop the VM and analyze the disk and load the snapshot and analyze the disk..
2. create a instance with a zonal persistent SSD disk, configure stackdriver agent and enable monitoring, configure the local SSD, save few data, take a snapshot, , validate the disk attached - boot device and local device, restart the VM and analyse the disk, stop the VM and analyze the disk and load the snapshot and analyze the disk.
3. create a new vm from the above snapshots.

## Solution

### 1

- Create instance
  - label: Storage: local
  - Series: First generation - N1
  - Machine type: n1-standard-1
  - boot disk: Debian GNU/Linux 10
  - allow http/https
  - disk: select local disk, number of disk 1, not auto snapshot

```sh
# install stackdriver sgent on the VM
curl -sSO https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh
sudo bash add-monitoring-agent-repo.sh
sudo apt-get update
sudo apt-get install stackdriver-agent
sudo service stackdriver-agent start
sudo service stackdriver-agent status

# validate stackdriver dashboard, disk section with filter device:sdb

lsblk
#NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
#├─sda1    8:1    0  9.9G  0 part /
#sda       8:0    0   10G  0 disk
#├─sda14   8:14   0    3M  0 part
#└─sda15   8:15   0  124M  0 part /boot/efi
#sdb       8:16   0  375G  0 disk

sudo mkfs.ext4 -F /dev/sdb
#mke2fs 1.44.5 (15-Dec-2018)
#Discarding device blocks: done
#Creating filesystem with 98304000 4k blocks and 24576000 inodes
#Filesystem UUID: 5dce72da-5a8e-41d0-880f-37017c070e7f
#Superblock backups stored on blocks:
# 32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
# 4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968
#
#Allocating group tables: done
#Writing inode tables: done
#Creating journal (262144 blocks): done
#Writing superblocks and filesystem accounting information: done

sudo mount /dev/sdb /mnt/disks/localSSD/

sudo touch /mnt/disks/localSSD/{file1,file2,file3} # enter some text in any of the file

sudo blkid
#/dev/sda1: UUID="26b22f51-cd73-4dde-88da-19ccef660ed4" TYPE="ext4" PARTUUID="12c4a9bc-d03e-450a-a054-bd4803b2673a"
#/dev/sda14: PARTUUID="a41eb064-c329-4845-89c3-4447eeb00012"
#/dev/sda15: SEC_TYPE="msdos" UUID="FCCD-070B" TYPE="vfat" PARTUUID="d1448047-26af-4e2c-a713-e0e075030e19"
#/dev/sdb: UUID="5dce72da-5a8e-41d0-880f-37017c070e7f" TYPE="ext4"

cat /etc/fstab # last line is entered for making the mount permanent
# /etc/fstab: static file system information
#UUID=26b22f51-cd73-4dde-88da-19ccef660ed4 / ext4 rw,discard,errors=remount-ro 0 0
#UUID=FCCD-070B /boot/efi vfat defaults 0 0
#UUID=5dce72da-5a8e-41d0-880f-37017c070e7f /mnt/disks/localSSD ext4 rw,discard,errors=remount-ro 0 0

# Suspend a VM with localSSD will persistent the data locally.

# Stopping a VM is not allowed when it uses local storage.
```

### 2

```sh
# same process as above the only difference is between after stop or deleting we can access the files those are saved in persistent disk.
```

### 3

```sh
# create a VM from snapshot of VM-with-localSSD
# instead of selecting the default boot disk, choose from the snapshot.
```
