# File Store

- Save file persistently and share between VMs.
- Its like NAS (network attached storage).
- This is mostly use when we migrate legacy application in Google cloud, which required access to file system similar to on premise environment.

- Can be accessed from compute engine and GKE.

- Its exposes NFS fileshare with fixed export settings and default Unix permissions.
- They can be available as mount points in GCE VMs.

- When we write data to File store they are automatically stored in other zones for maintaining redundancy.

- Also encrypts data while they are in transit.
