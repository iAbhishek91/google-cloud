Auth

## Create a cluster

```sh
gcloud beta container --project "nice-beanbag-288720" clusters create "analytics" --zone "europe-west2-a" --no-enable-basic-auth --cluster-version "1.16.15-gke.4300" --machine-type "e2-medium" --image-type "COS" --disk-type "pd-standard" --disk-size "30" --metadata disable-legacy-endpoints=true --scopes "https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --preemptible --num-nodes "1" --enable-stackdriver-kubernetes --enable-ip-alias --network "projects/nice-beanbag-288720/global/networks/default" --subnetwork "projects/nice-beanbag-288720/regions/europe-west2/subnetworks/default" --default-max-pods-per-node "110" --no-enable-master-authorized-networks --addons HorizontalPodAutoscaling,HttpLoadBalancing --enable-autoupgrade --enable-autorepair --max-surge-upgrade 1 --max-unavailable-upgrade 0 --workload-pool "nice-beanbag-288720.svc.id.goog"
```

## Create Kubernetes service account

```sh
k create ns <<google-authorised>>

k create sa -n <<google-authorised>> <<google-sa>>
```

## Create Google service account

```sh
gcloud iam service-accounts create <<api-access>>
```

## Bind service account of Google and Kubernetes

Allow the Kubernetes service account to impersonate the Google service account by creating an IAM policy binding between the two. This binding allows the Kubernetes Service account to act as the Google service account.

```sh
gcloud iam service-accounts add-iam-policy-binding \
--role roles/iam.workloadIdentityUser \
--member "serviceAccount:<<nice-beanbag-288720.svc.id.goog[<<google-authorised>>/<<google-sa>>]” \
<<api-access>>@<<nice-beanbag-288720>>.iam.gserviceaccount.com
```

```sh
k annotate sa --namespace google-authorised   google-sa  iam.gke.io/gcp-service-account=api-access@nice-beanbag-288720.iam.gserviceaccount.com
```

## Test by creating the below pod in GKE cluster

```sh
k run -it --image google/cloud-sdk:slim -sa google-sa -n google-authorised workload-identity-test

gcloud auth list
```

> Ref: https://cloud.google.com/kubernetes-engine/docs/how-to/workload-identity#kubectl_1
