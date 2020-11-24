# CD using Spinnaker

## Steps

### 1. Create a kubernetes cluster

```sh
gcloud config set compute/zone us-central1-f

gcloud container clusters create spinnaker-tutorial \
    --machine-type=n1-standard-2
```

### 2. Configure IAM

```sh
gcloud iam service-accounts create spinnaker-account \
    --display-name spinnaker-account

# Create some env variable required later
export SA_EMAIL=$(gcloud iam service-accounts list \
    --filter="displayName:spinnaker-account" \
    --format='value(email)')

export PROJECT=$(gcloud info --format='value(config.project)')

# Bind storage admin role to svc account
gcloud projects add-iam-policy-binding $PROJECT \
    --role roles/storage.admin \
    --member serviceAccount:$SA_EMAIL

# Create a ssh key for the service account - the below command will also download the key in the current folder
gcloud iam service-accounts keys create spinnaker-sa.json \
     --iam-account $SA_EMAIL
```

### 3. Configure cloud pub/sub

Pub/Sub is required for creating trigger the events - notification from container-registry

```sh
# Create pub/sub topic
gcloud pubsub topics create projects/$PROJECT/topics/gcr

# Create a subscription that Spinnaker can read from to receive notifications of images being pushed
gcloud pubsub subscriptions create gcr-triggers \
    --topic projects/${PROJECT}/topics/gcr

## Authorizing the subscription to be read by spinnaker

export SA_EMAIL=$(gcloud iam service-accounts list \
    --filter="displayName:spinnaker-account" \
    --format='value(email)')

gcloud beta pubsub subscriptions add-iam-policy-binding gcr-triggers \
    --role roles/pubsub.subscriber --member serviceAccount:$SA_EMAIL
```

### 4. Install Spinnaker

```sh
# Create cluster role binding for cluster-admin
kubectl create clusterrolebinding --clusterrole=cluster-admin \
    --serviceaccount=default:default spinnaker-admin

# Configuring helm with the chart repo
./helm repo add stable https://kubernetes-charts.storage.googleapis.com
./helm repo update

# Configure few env variable
export PROJECT=$(gcloud info \
    --format='value(config.project)')
export BUCKET=$PROJECT-spinnaker-config

gsutil mb -c regional -l us-central1 gs://$BUCKET

# Spinnaker-config.yaml
export SA_JSON=$(cat spinnaker-sa.json)
export PROJECT=$(gcloud info --format='value(config.project)')
export BUCKET=$PROJECT-spinnaker-config
cat > spinnaker-config.yaml <<EOF
gcs:
  enabled: true
  bucket: $BUCKET
  project: $PROJECT
  jsonKey: '$SA_JSON'

dockerRegistries:
- name: gcr
  address: https://gcr.io
  username: _json_key
  password: '$SA_JSON'
  email: 1234@5678.com

# Disable minio as the default storage backend
minio:
  enabled: false

# Configure Spinnaker to enable GCP services
halyard:
  additionalScripts:
    create: true
    data:
      enable_gcs_artifacts.sh: |-
        \$HAL_COMMAND config artifact gcs account add gcs-$PROJECT --json-path /opt/gcs/key.json
        \$HAL_COMMAND config artifact gcs enable
      enable_pubsub_triggers.sh: |-
        \$HAL_COMMAND config pubsub google enable
        \$HAL_COMMAND config pubsub google subscription add gcr-triggers \
          --subscription-name gcr-triggers \
          --json-path /opt/gcs/key.json \
          --project $PROJECT \
          --message-format GCR
EOF

# install spinnaker using helm
./helm install -n default cd stable/spinnaker -f spinnaker-config.yaml \
           --version 2.0.0-rc9 --timeout 10m0s --wait
```

### 5. Host Spinnaker

```sh
export DECK_POD=$(kubectl get pods --namespace default -l "cluster=spin-deck" \
    -o jsonpath="{.items[0].metadata.name}")
  
kubectl port-forward --namespace default $DECK_POD 8080:9000 >> /dev/null &
```

### 6. Working with codebase

```sh
gsutil -m cp -r gs://spls/gsp114/sample-app.tar .

mkdir sample-app
tar xvf sample-app.tar -C ./sample-app

cd sample-app

# change user name
git config --global user.email "$(gcloud config get-value core/account)"
git config --global user.name "[USERNAME]"

# Initial commit
git init
git add -A
git commit -m "initial commit"

# Create a source repo in GCP and push. (you may be billed for the registry)
gcloud source repos create sample-app

git config credential.helper gcloud.sh

export PROJECT=$(gcloud info --format='value(config.project)')
git remote add origin https://source.developers.google.com/p/$PROJECT/r/sample-app

git push origin master
```

### 7. Configure build trigger

Git trigger should be created whenever there is a git tag created.

*Configure Container Builder to build and push your Docker images every time you push Git tags to your source repository. Container Builder automatically checks out your source code, builds the Docker image from the Dockerfile in your repository, and pushes that image to Google Cloud Container Registry.*

```sh
Navigation Cloud build >> cloud build >> Triggers : click "Create Trigger"

Name: sample-app-tags
Event: Push new tag
Select repe: sample-app
Tag: v.*
Build configuration: Cloud Build configuration file (yaml or json)
Cloud Build configuration file location: /cloudbuild.yaml

# From now on when you create a tag which starts with v.* it will create a image in the container registry

# Contain of cloudbuild is pasted below, however you can build using 
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '--tag=gcr.io/$PROJECT_ID/sample-app:$TAG_NAME', '.']
- name: 'gcr.io/cloud-builders/docker'
  args: ['run', 'gcr.io/$PROJECT_ID/sample-app:$TAG_NAME', 'go', 'test']
- name: 'gcr.io/cloud-builders/gsutil'
  args: ['cp', '-r', 'k8s/*', 'gs://$PROJECT_ID-kubernetes-manifests']
images: ['gcr.io/$PROJECT_ID/sample-app:$TAG_NAME']
```

### 8. K8s Manifest required by spinnaker

*Spinnaker needs access to your Kubernetes manifests in order to deploy them to your clusters. This section creates a Cloud Storage bucket that will be populated with your manifests during the CI process in Cloud Build. After your manifests are in Cloud Storage, Spinnaker can download and apply them during your pipeline's execution.*

```sh
export PROJECT=$(gcloud info --format='value(config.project)')

gsutil mb -l us-central1 gs://$PROJECT-kubernetes-manifests

# Versioning is required, so that we can keep track of the manifest we are using
gsutil versioning set on gs://$PROJECT-kubernetes-manifests

sed -i s/PROJECT/$PROJECT/g k8s/deployments/*
git commit -a -m "Set project ID"
git tag v1.0.0
git push --tags
```

### 9. CLI for Spinnaker

```sh
# Download spin
curl -LO https://storage.googleapis.com/spinnaker-artifacts/spin/1.14.0/linux/amd64/spin
chmod +x spin

# create a application
./spin application save --application-name sample \
                        --owner-email "$(gcloud config get-value core/account)" \
                        --cloud-providers kubernetes \
                        --gate-endpoint http://localhost:8080/gate

# create a pipeline
## will determine the docker image which starts with v.* and trigger the pipeline
export PROJECT=$(gcloud info --format='value(config.project)')
sed s/PROJECT/$PROJECT/g spinnaker/pipeline-deploy.json > pipeline.json
./spin pipeline save --gate-endpoint http://localhost:8080/gate -f pipeline.json
```

- Now we can manually trigger the build, or can execute via trigger.

- the pipeline is stores everything. It reads the change in cloud registry and triggers the build.
