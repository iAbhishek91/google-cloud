# Big Query

> NOTE: Big Query is not listed under storage section as this service sits in between data storage and data processing.

Big Query is a warehouse database. Used for enterprise data warehouse.

BigQuery helps to running queries, loading data, and even creating and training ML models. Check out Big Queries.

## Create a data set

Just create a data-set in bigQuery.

- name: doctord_could_bills
- location: eu-west2

### Which data storage service provides data warehouse services for storing data but also offers an interactive SQL interface for querying the data

Big Query

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
