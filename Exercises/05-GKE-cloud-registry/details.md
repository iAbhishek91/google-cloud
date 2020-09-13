# GKE and cloud registry

create a docker image using cloud build and upload into registry.

## scenario

Create dockerfile and deploy into container registry using cloud build. Deploy that image as pod and see the deployment in stack driver.

## solution

```sh
# verify the API are enabled
gcloud services list --enable | grep cloudbuild

# get the complete name of the api
gcloud services list --available | grep cloudbuild

# enable cloud build API
gcloud services enable cloudbuild.googleapis.com

# verify the API are enabled
gcloud services list --enable | grep containerregistry

# create file date.sh
sudo vi date.sh
#!/bin/bash
echo "Hello, the time is $(date)"

# create a Dockerfile
FROM alpine
cp date.sh /
cmd ["/date.sh"]

# now build the image in cloud build
# the above command will build and upload the image in GCR
gcloud build submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/date-image .

# execute build using config file
gcloud builds submit --config cloudbuild.yaml .
```

## sample build configuration file

gcloud builds submit --config cloudbuild.yaml .

```yaml
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: [ 'build', '-t', 'gcr.io/$PROJECT_ID/date-image', '.' ]
images:
- 'gcr.io/$PROJECT_ID/date-image'
```

gcloud builds submit --config cloudbuild.yaml .

```yaml
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: [ 'build', '-t', 'gcr.io/$PROJECT_ID/quickstart-image', '.' ]
- name: 'gcr.io/$PROJECT_ID/quickstart-image'
  args: ['fail']
images:
- 'gcr.io/$PROJECT_ID/quickstart-image'
```
