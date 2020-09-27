# Enable API for new project

- We will enable API service of
  - compute engine [compute.googleapis.com]
  - kubernetes engine [container.googleapis.com]
  - container registry [containerregistry.googleapis.com]
  - app engine [appengine.googleapis.com]
  - cloud function [cloudfunctions.googleapis.com]
  - storage [storage-component.googleapis.com]
  - cloud run [run.googleapis.com]
  - cloud build [cloudbuild.googleapis.com]
  - stack driver [stackdriver.googleapis.com]

- Navigate to *API and services*
- Then to libraries, search by compute

```sh
# enabled services or API
gcloud services list

# all services
gcloud services list --available

# enable a service
gcloud services enable compute.googleapis.com
gcloud services enable container.googleapis.com containerregistry.googleapis.com
gcloud services enable cloudbuild.googleapis.com
gcloud services enable run.googleapis.com
gcloud services enable storage-component.googleapis.com
gcloud services enable stackdriver.googleapis.com
```

> Note: API are enabled GCP will automatically create service accounts for you. You may use the default service account or create your own.
