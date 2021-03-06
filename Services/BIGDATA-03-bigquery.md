# Big Query

> NOTE: Big Query is not listed under storage section as this service sits in between data storage and data processing.

- Big Query is a multi-cloud warehouse database. Used for enterprise data warehouse.
- fully managed, serverless, very fast, highly scalable & cost effective service.
- *Petabyte scale*, we can load huge data in big query for analysis.
- has SQL interface.
- free tier to start with.

BigQuery helps to running queries, loading data, and even creating and training ML models. Check out Big Queries.

## Long term storage

Big Query have a similar option like cloud storage near line, if you don't access data for 90 days then price of the data is automatically dropped to $0.01/GB.

## Load data in BigQuery

- Batch
- Stream individual or in batches: consider the limitation in the .
- Use queries to generate new data.
- Use 3rd party.

## Policy tagging for security

https://cloud.google.com/bigquery/docs/best-practices-policy-tags

## Exploratory queries

- Explore new data coming to big-query, using exploratory queries.
- fully managed and scalable
- you can query big-query without knowing to know what you are looking for.

## Big query

- Schedule queries or transfer data from SaaS application to google bigQuery on a regular basis.

For example, you want to analyse google adward real time data in bigQuery.

https://cloud.google.com/bigquery-transfer/docs/reference/datatransfer/rest

## Create a data set

Just create a data-set in bigQuery.

- name: doctord_could_bills
- location: eu-west2

## interact with BigQuery

Cloud console | Cloud  shell | API

## Few examples of queries

```sql
/*
dataset: imported_billing_data
table: sampleinfotable
*/
select * from imported_billing_data.sampleinfotable where Cost > 0;



SELECT
  product,
  resource_type,
  start_time,
  end_time,
  cost,
  project_id,
  project_name,
  project_labels_key,
  currency,
  currency_conversion_rate,
  usage_amount,
  usage_unit
FROM
  `cloud-training-prod-bucket.arch_infra.billing_data`
WHERE
  Cost > 0
ORDER BY end_time DESC
LIMIT
  100


/*To find the most frequently used product costing more than 1 dollar,*/
SELECT
  product,
  COUNT(*) AS billing_records
FROM
  `cloud-training-prod-bucket.arch_infra.billing_data`
WHERE
  cost > 1
GROUP BY
  product
ORDER BY
  billing_records DESC

/*To find the most commonly charged unit of measure */
SELECT
  usage_unit,
  COUNT(*) AS billing_records
FROM
  `cloud-training-prod-bucket.arch_infra.billing_data`
WHERE cost > 0
GROUP BY
  usage_unit
ORDER BY
  billing_records DESC


/*To find the product with the highest aggregate cost*/
SELECT
  product,
  ROUND(SUM(cost),2) AS total_cost
FROM
  `cloud-training-prod-bucket.arch_infra.billing_data`
GROUP BY
  product
ORDER BY
  total_cost DESC
```
