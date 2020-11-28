# bq

```sh
# create a data-set
export PROJECT_ID=$(gcloud info --format='value(config.project)')
bq mk --project_id $PROJECT_ID flights
```
