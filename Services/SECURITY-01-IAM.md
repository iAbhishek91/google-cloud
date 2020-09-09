# IAM

Googles Identity manager, which manages **who** can do **what** for **which** resources.

> Best practice **least privilege environments** should be followed and IAM help in achieving that.

## Three part of IAM policies

- **Who**(identities/members) : individual users(google account | service account) or google group (collection of users) or cloud identity domain(org who do not have G suite can use this) or entire g-suite domain or alias *allAuthenticatedUsers* or anonymous users *allUsers*.
- can do **what**(roles) : collection of permissions (start, stop, create, delete) grouped together in a role (dev, admin, reporter ).
- on **which**(permissions) :  operation performed on a specific resources. Under the hood they corresponds to REST method of GCP resources(Publisher.Publish() -> pubsub.topics.publish).For eg: create a VM, list a VM etc.

> NOTE: Permissions are structured in format service.resource.verb
> NOTE: Permission CANNOT be assigned directly to members or users. It need to be grouped in roles and then assigned to identities.

## Different types of roles

- **Primitive** : they are fixed coarse-grained level of access (*owner*, *editor*, *viewer*, owner can also setup billing). They are not suggested for live landscape. Primitive roles are applied to all resources.
- **Predefined** : they are defined by GCP based on the services and are not applied on all resources.
- **Custom** : can be created by users from IAM. Custom rules can only be applied at project and organization level and cant be applied to folder level.

## Service users(accounts)

- Service accounts belongs to application or VM.
- They have unique email address created by GCP in specific nomenclature.
- Service ac are associated with key-pairs used for authentication.
- Service user are resources too and need to be managed. Roles can be applied to them.
- In case a VMs need access to other VMs, we can create service accounts and give them appropriate permissions to manage the VMs.
- Allows to authenticate between GCP services.
- Allow user to act with permission defined for a service account.

- Two type of service accounts:
*User managed* and *Google managed*
- Once we create project, set of service accounts are automatically created (should not delete them). These are called *Google managed* svc ac.

### Creating service account

- enter name, email is auto created.
- assign roles on next steps.
- create a key for the svc account. This will generate a JSON (recommended way) and that gets downloaded to local system. Basically its a SSH private key.
