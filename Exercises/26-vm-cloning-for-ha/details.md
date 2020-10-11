# Cloning VM

Create a copy of a VM in another region for HA

## Steps

**Step-1** Create a VM

- name: first-vm
- zone: europe-west2-a

**Step-2** Make some changes to identify the vm.

- create a directory and keep some files

```sh
sudo mkdir -p /abhishek/testing
sudo touch /abhishek/testing/file{1,2}
```

**Step-3** Create a snapshot of the VM

- name: first-instance-snapshot
- region- us-central1

**Step-4** create a disk from that snapshot (this is optional - an instance boot disk can be snapshot as well)

- name: second instance
- region: us-cental1 (not dependent on snapshot region)
- source type: first-instance-snapshot

**Step-5** Create a VM from that disk as boot disk

*Before creating the VM: you may delete the VM instance(step-1) and the snapshot(step-3)*.

change the boot disk to the above disk available.

> NOTE: the region of the disk and the VM should be same.If you are directly using a snapshot, then Snapshot should be on the same zone.
