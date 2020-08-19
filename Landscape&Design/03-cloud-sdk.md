# Google cloud SDK

SDK provides with interfaces to interact with the resources.

Generally SDK comes in different form to support multiple environments (like Java, NodeJS, CLI).

CLI form of SDK is installed on cloud shell, hence we can just use it.

SDK available for local use as well, hence we can use it from local system.

## SDK commands

### gcloud

- This command interact with GCP services.
- They are organized in groups to interact with different services.
- Each groups refer to resource types.
- Each resource type refer to actions

For Example:

- list instances resources: `gcloud compute instances list`
- stop a vm `gcloud compute instances stop <instance-id>`
- lists all the possible actions on instances `gcloud compute instances`
- lists all the possible actions on disk`gcloud compute disk`

### gsutil

Used to work with storage. Note Storage is just a object repo, which stores unstructured data. *This commands are linux based commands*

For Example:

- list all the buckets: `gsutil ls`
- list all the commands available: `gsutil help`

## bq

Command used to work with `Big Query`

For Example:

- list all the commands available: `bq help`.

## cbt

Command to work with `cloud big table`

For example:

- list all the commands available: `cbt help`
