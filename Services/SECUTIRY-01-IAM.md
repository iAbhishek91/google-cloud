# IAM

Googles Identity manager, which manages who can do what.

- best practice **least privilege environments** should be followed and IAM help in achieving that.

## Three part of IAM policies

- Who : individual users(google account | service account) or google group or cloud identity or entire g-suite
- Can do what : collection of permissions (start, stop, create, delete) grouped together in a role (dev, admin, reporter ).
- On which resources :

## Different types of roles

- Primitive : they are fixed coarse-grained level of access (owner, editor, viewer, owner can also setup billing). They are not suggested for live landscape. Primitive roles are applied to all resources.
- Predefined : they are defined by GCP based on the services and are not applied on all resources.
- Custom : can be created by users from IAM. Custom rules can only be applied at project and organization level and cant be applied to folder level.

## Service users

- Service user are resources too and need to be managed. Roles can be applied to them.
- In case a VMs need access to other VMs, we can create service accounts and give them appropriate permissions to manage the VMs.
- Allows to authenticate between GCP services.
- Allow user to act with permission defined for a service account.
