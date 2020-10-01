# IAM

Googles Identity manager, which manages **who** can do **what** for **which** resources.

> Best practice **least privilege environments** should be followed and IAM help in achieving that.
> IAM can NOT create user or group in GCP, instead gsuite or cloud identity is used. IAM can only create a service account.

## Policies

- **Policies** are NOT a resources by themselves, but are combination of *identities/members* and *roles* with *few optional condition like expiry date..
- Google- definition: *A Policy is a collection of bindings. A binding binds one or more members to a single role. Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A role is a named list of permissions; each role can be an IAM predefined role or a user-created custom role*
- Polices are inherited from the parent. Each resources can have only one parent.

### Three part of IAM policies

- **Who**(identities/members) : individual users(google account | service account) or google group (collection of users) or cloud identity domain(org who do not have G suite can use this) or entire g-suite domain or alias *allAuthenticatedUsers* or anonymous users *allUsers*.
- can do **what**(actions/verb) : collection of permissions (start, stop, create, delete) grouped together in a role (dev, admin, reporter ).
- on **which**(resources) :  operation performed on a specific resources. Under the hood they corresponds to REST method of GCP resources(Publisher.Publish() -> pubsub.topics.publish).For eg: create a VM, list a VM etc.

> NOTE: *Which* and *What* combines together to form
> NOTE: Permissions are structured in format *service*.*resource*.*verb*
> NOTE: Permission CANNOT be assigned directly to members or users. It need to be grouped in roles and then assigned to identities.

## IAM objects

There are different objects that consist of IAM

- Organizations (refer landscape and design > Project.md)
- Folders (refer landscape and design > Project.md)
- Projects (refer landscape and design > Project.md)
- Members
  - google accounts *any@gmail.com*,
  - any other account from other domain *any@example.com*
  - google group *any@googlegroup.com*,
  - service accounts *any@cloudervices.gserviceaccount.com*,
  - cloud identity or g-suit domain *any@example.com*
- Roles
- Resources

> NOTE: Separate IAM roles are defined for person managing Projects(admin/owner or deleter), folders (owner, creator, viewer) and organization(create, viewer)

## Different types of roles

- **Primitive** : they are fixed coarse-grained level of access (*owner*, *editor*, *viewer*, owner can also setup billing *billing administrator*). They are not suggested for live landscape. Primitive roles are applied to all resources.
- **Predefined** : they are defined by GCP based on the services and are not applied on all resources.
- **Custom** : can be created by users from IAM. Custom rules can only be applied at project and organization level and CANT be applied to folder level.

> NOTE: while creating a custom role we can version them as alpha, beta, general availability and disabled. Start with alpha.
> NOTE: Also since they are not managed by Google, this roles will never get updated automatically.

## Service users(accounts)

- Service accounts belongs to application or VM.
- They have unique email address created by GCP in specific nomenclature.
- Service ac are associated with key-pairs used for authentication. User need to create the key, the private key is downloaded when the key creation is completed.
- Service user are resources too and need to be managed. Roles can be applied to them.
  - As service accounts are resource user/group can have access to use the service account. *If user or group do not have permission to access the service account, they will not be able to use the service account. Indirectly restricting the roles assigned to service accounts to the users (assume roles cant be accessed directly to user in your setup.). In another way we can say that service accounts are way to assign privileges to users*
- In case a VMs need access to other VMs, we can create service accounts and give them appropriate permissions to manage the VMs.
- Allows to authenticate between GCP services.
- Allow user to act with permission defined for a service account.

### Creating service account

- There are three types of services accounts:
  - *Built in svc account* : they an use primitive and pre-defined roles.
  - *Google API svc account*: Runs google internal services on behalf of users. They have editor role in the project.
  - *user created*:
    - enter name, email is auto created.
    - assign roles on next steps.
    - create a key for the svc account. This will generate a JSON (recommended way) and that gets downloaded to local system. Basically its a SSH private key.
    - can only use pre-defined roles.

### How are service account authenticated

Services a/cs are authenticated using SSH keys. There are two type of keys *Google managed keys* (cant be downloaded, and automatically rotated), and *User managed keys* (can be downloaded, managed and rotated)

## Access Scope

- Each service also come with scope apart from User roles. *For example: one project-a have read-only access to cloud storage and another have read-write, hence same user will have different access token from the authorization token from the authorization server for accessing the cloud storage.*.
- Before making any call to the Google service API, **Authorization server** is contacted for fetching the token for accessing the API.
- Accessed scope can be defined when we create a instance.
- Access scope can be modified by stopping the instances.

## From different corporate directory

### Using Google cloud directory

If your organization is using Microsoft Ad or LDAP, GCP can **schedule one-way sync using google cloud directory sync to google cloud identity domain**. Both users and groups can be copied.

In this case user can use GCP with the same username and password to access the GCP.

### Using SSO

Use client identity to configure SAML SSO.
If SAMl 2 is not supported, use a third party solution (ADFs, Ping, Okta).

Below three details are required to configure the SAML SSO:

- Sign in page URL: Sign in page URL and G-suite
- Sign out page URL: URL for redirecting users when they signout
- Change password URL: URL to change your password
- SSL Certificates.

> SSO is redirecting to one common authentication platform and granting permission to the base site. Basically authorization is delegated.

### Quotas

- This services prevents from over consumption of resources. Configure limit on resources used.
- Quotas are allocated on project levels.
- Two different type of quotas:
  - **Rate quotas**: (for example: 1000 requests per 10 seconds)
  - **Allocation quotas**: (for example: 5 network per project)
- to change quotas, we need to request from the IAM and update. This change request is free of cost. Some needs request to GCP support team. we can also change th quotas from CLI.

## Best practices for IAM

- Understand the resource hierarchy.
- Create project to group resources that share same trust boundary.
- Check the policy granted to each resources and make sure you understand the inheritance.
- Use the principal of *least privilege*.
- Audit policies in cloud audit logs.
- Audit membership of groups used in policies.
