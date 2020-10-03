# Running VM as svc account

Running VM as service account.

Owner creates a VM, with a custom svc account. Now the owner have its own IAM roles as well as the svc account have its roles.

Now, if a VM instance is created with a svc account the svc account roles are applied in the VM automatically.

By default, *gcloud* and *gsutil* tools are authorized automatically, however for custom tools and application manually srv account need to be authenticated.

> NOTE: if user permissions can be elevated using svc account, so svc account user(user who can use this svc account) and svc account admin(user who can manage the svc account) must be selected correctly.

## Creating a VM as a service account

- First step we need to create a svc account.
- Create a VM with the service account.
- perform  a task which are not authorized. 403 error should be displayed.
