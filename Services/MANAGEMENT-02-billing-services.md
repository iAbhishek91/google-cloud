# Billing services

These services helps you to manage the cost and provide dashboard for viewing the GCP bills.

> Refer example: 10-Basic-project-user-API-stackdriver-billingAC/02-configure-billing.md

## Billing Account

- This is account act as a billing administrator.
- To change a billing account of a project one need owner access and a billing administrator on the billing account.
- Every functional projects are linked to billing accounts. If a project with no billing account can use only free GCP services.
- If you have one billing account, then automatically all project are linked to billing account.
- If you don't have a billing account you must create one to consume service.
- Billing accounts are linked to one or more projects.
- GCP charge automatically or invoiced every month or at threshold limit.
- Additionally we can create sub accounts to separate billing for a project.

## Budget and alerts

- Configure budget per GCP billing account or per GCP projects.
- Budget can be a fixed limit or can tie it to a another metric(% of previous month spend).
- Create an alert when bill reaches your budget limits.
- To create budget alert, you must be a billing administrator.
- We can also configure web-hooks with alerts to shut down resource, or create a JIRA ticket anything.

> NOTE: Setting a budget does not cap API usage.

## Billing export

It helps you to store the detail billing details in a location where it is easy to retrieve. (Two types: BigQuery or cloud storage.) These information can be later utilized for analytics.

- Big Query: sends you billing data to a BigQuery data sheet.
  - you can send the pricing.
  - you can send the Daily cost details
- 

## Quotas

- This services prevents from over consumption of resources. Configure limit on resources used.
- Quotas are allocated on project levels.
- Two different type of quotas:
  - **Rate quotas**: (for example: 1000 requests per 10 seconds)
  - **Allocation quotas**: (for example: 5 network per project)
- to change quotas, we need to request from the IAM and update. This change request is free of cost. Some needs request to GCP support team. we can also change th quotas from CLI.
