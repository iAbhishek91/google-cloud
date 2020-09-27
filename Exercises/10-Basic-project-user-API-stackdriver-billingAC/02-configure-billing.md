# configure billing account

## Create a billing account

- search for *billing*
- create a billing account, by navigating to billing account management, create new account
  - name: anything
  - country: United kingdom
  - currency(readonly): GBP
  - Payment profile: create a new or use the existing one.
    - Account type(read only): individual
    - Name and address: *edit if required*
    - how to pay(read only): monthly when payment is due
    - payment method: debit/credit card details

## Change the billing account of the project "doctor D"

> for changing billing one must have link and unlink permission of projects with billing account.

Add yourself *project billing manager*, *Billing Account Usage Commitment Recommender Admin*

- from billing of old billing account >> Account management
- click on three dots >> change billing
- select the new billing account.

> NOTE: you can change or disable account from any of these.

## Create budget and alerts

- Enter a budget name: doctorsd budget
- Scope:
  - all project this billing account is assigned with.
  - products
- Amount:
  - Budget type: specified amount
  - Target amount: £5
  - Include credits in cost: true
- Actions:
  - 50% | £2.5 | Trigger on actual budget
  - 80% | £4   | Trigger on actual budget
  - 100%| £5   | Trigger on forecasted budget
- Alerts
  - Email alerts to billing admins and users.

## Budget export

- Select Billing export
- Select BigQuery export
- Edit settings of daily cost details
  - Project Name: Doctor D
  - Dataset name: doctord_cloud_bills (create bigquery data set separately prior to this step)
