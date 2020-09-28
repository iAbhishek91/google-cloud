# Share a service accounts between multiple projects

Share a single service account between multiple projects.

>Note: service account is project wise resources.

## Steps

- Create a svc ac.
- Copy the email id of the svc account.
- Navigate to second project:
- add the svc account user as normal user.
- grant them permission as required.

## Use cases

This pattern can be particularly useful when you have a separate project for implementing automation or monitoring tasks that span multiple projects and need to have access to them. Following the steps above, you can grant the source project access to perform the required actions in other projects.
