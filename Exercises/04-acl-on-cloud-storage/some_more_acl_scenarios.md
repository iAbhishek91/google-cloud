# Some self created scenarios

## SCENARIO-I

**NOTE: this is NOT an example of ACL on cloud storage, its an ACL on Compute engine.**
Restrict access of storage by creating VM as svc accounts.

### Steps

- create a svc account, with storage viewer.
- create a VM using this service account.
- access a storage using `gsutil ls gs://sorage_name` : this action should be successful
- copy another file to storage `gsutil cp file1 gs://storage_name`: 403 as svc account is not having access.

> NOTE: the user logged into the VM using ssh is the owner of the project, but since the VM is created with the svc account(also termed as VM as svc ac) svc account roles are applied.

## SCENARIO-II

Assign ACL to cloud storage bucket and object.

### Steps

- click on the `edit permission` on the bucket. Add member (the above svc account) and select `storage object creator` role.
- similarly click on one of the objects `edit permission`. Add `entity` (user, project, group, public etc) | `name` (email id in this case) | access (reader or owner). and delete all the other files.
- validate the acl of the objects `gsutil acl gs://url/file1` | `gsutil acl gs://url/file2` | `gsutil acl gs://url/file3`. svc ac have reader role should be mentioned there for one object.
- create a VM with svc ac hae role of `storage admin`
- try to access the objects and delete the object which have read-only.
  - authorized:
  - not authorized: 
- Verify that the object that is have READ ACL defined will throw 403.
