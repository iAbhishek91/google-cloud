# Billing services

These services helps you to manage the cost and provide dashboard for viewing the GCP bills.

## Biller Account

- This is account act as a billing administrator.
- To change a billing account of a project one need owner access and a billing administrator on the billing account.
- Projects are linked to billing accounts.
- If you have one billing account, then automatically all project are linked to billing account.
- If you don't have a billing account you must create one to consume service.

## Budget and alerts

- Configure budget per GCP billing account or per GCP projects.
- Budget can be a fixed limit or can tie it to a another metric(% of previous month spend).
- Create an alert when bill reaches your budget limits.
- To create budget alert, you must be a billing administrator.

> NOTE: Setting a budget does not cap API usage.

## Billing export

It helps you to store the detail billing details in a location where it is easy to retrieve. (For example: BigQuery or cloud storage.) These information can be later utilized for analytics.

## Quotas

- This services prevents from over consumption of resources. Configure limit on resources used.
- Quotas are allocated on project levels.
- Two different type of quotas:
  - Rate quotas: (for example: 1000 requests per 10 seconds)
  - Allocation quotas: (for example: 5 network per project)
- to change quotas, we need to request to google support team.
