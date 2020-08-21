# Projects

## What are projects

- Projects are cloud resources that are managed as an administrative unit.
- There are limits (23) in the number of project we can create by default. It can be increased by requesting GCP.
- We can group resources which have common business objectives. **resources >> VMs**
- optionally this projects can be organized into folders and other folders. **folders >> ... >> folders >> resources >> VMs**
- folders my represent - departments, env, teams etc.
- resources under a folder including projects and resources inherits policies from the parent folder.
- every folders, project can be brought together under a organization node. **org node >> folders >> ... >> folders >> resources >> VMs**
- when we use folders, organization node is mandatory.
- fine grain roles are defined at organization layer. Organization policy administrator, project creator.
- in every layer policies can be applied and the polices are implied downward.

> NOTE: if you have owner permission on project, and the resource is restricted with more stronger policy. Then the owner will still have owner rights to all the resources.

## How to access Projects

- from console top menu bar. Beside Google Cloud Platform. From the project selectors.
- From project selector, we can view the existing projects or create a new project if required.

## Projects identifying attributes

- Project ID (globally unique, chosen by customer, immutable)
- Project Name (can be anything, chosen by customer, immutable)
- Project Number (globally unique, assigned by GCP, immutable)

## How to create an organization node

Answer depends on if your organization have a G-suite enrolled.

- if yes, automatically everything will be under an organization.
- else, you can use google cloud identity to create one.
