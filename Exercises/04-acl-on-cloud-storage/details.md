# Access control on cloud storage object

## Scenario

Create a bucket, copy a file in the bucket and make it restricted (access only to owner). Create a service account and grant him editor access. Authenticate the user in cloud shell and try to access the image. Validate the use will get permission issue.

Grant service account owner access and validate the use will give him permission issue as well.

## Solution

```sh
# Validate the iam API is enabled
gcloud services list --enabled | grep iam

# if not enable
gcloud services enable iam.googleapis.com

# create a service account
gcloud iam service-account create my-svc-ac --description="my service account" --display-name="my svc ac"

# validate the policies attached to project
gcloud projects get-iam-policy $GOOGLE_CLOUD_PROJECT

# fetch the email id of the service user which we created previously
gloud iam service-account list

# attach policy defining svc account with viewer role
gcloud projects add-iam-policy-binding $GOOGLE_CLOUD_PROJECT --member serviceAccount:my-svc-account@nice-beanbag-288720.iam.gserviceaccount.com --role roles/viewer

# create a standard bucket (dont give the retention option until you are sure, one will not be able to delete the storage)
gsutil mb --retention 1d -l Europe-West2 -p $GOOGLE_CLOUD_PROJECT -c standard gs://$GOOGLE_CLOUD_PROJECT

# list all the bucket available
gsutil ls

# copy a image from one to another
gsutil cp gs://cloud-training/ak8s/cat.jpg gs://nice-beanbag-288720/cat.jpg

# validate the image is copied
gsutil ls -l gs://nice-beanbag-288720

# validate the existing ACL on cat.jpg
gsutil act get gs://$GOOGLE_CLOUD_PROJECT/cat.jpg
#[
#  {
#    "entity": "project-owners-911427390672",
#    "projectTeam": {
#      "projectNumber": "911427390672",
#      "team": "owners"
#    },
#    "role": "OWNER"
#  },
#  {
#    "entity": "project-editors-911427390672",
#    "projectTeam": {
#      "projectNumber": "911427390672",
#      "team": "editors"
#    },
#    "role": "OWNER"
#  },
#  {
#    "entity": "project-viewers-911427390672",
#    "projectTeam": {
#      "projectNumber": "911427390672",
#      "team": "viewers"
#    },
#    "role": "READER"
#  },
#  {
#    "email": "abhi.das2007das@gmail.com",
#    "entity": "user-abhi.das2007das@gmail.com",
#    "role": "OWNER"
#  }
#]

# create acl on the object
## there are different way to do this, but below is the simplest
## Be careful, you should not accidentally remove owner permission
gsutil acl set private gs://$GOOGLE_CLOUD_PROJECT/cat.jpg
# Validate the acl post making it private
gsutil acl get gs://$GOOGLE_CLOUD_PROJECT/cat.jpg
#[
#  {
#    "email": "abhi.das2007das@gmail.com",
#    "entity": "user-abhi.das2007das@gmail.com",
#    "role": "OWNER"
#  }
#]

# authenticate the svc
gcloud auth activate-service-account my-svc-account@nice-beanbag-288720.iam.gserviceaccount.com --key-file=credentials.json --project=$GOOLGE_CLOUD_PROJECT
# validate the authenticated users
gcloud auth list
#ACTIVE  ACCOUNT
#        abhi.das2007das@gmail.com
#*       my-svc-account@nice-beanbag-288720.iam.gserviceaccount.com

# change the user to abhi.das2007das@gmail.com, for fun
gcloud config set account abhi.das2007das@gmail.com
# change it back to svc account
gcloud config set account my-svc-account@nice-beanbag-288720.iam.gserviceaccount.com

# try to delete the file cat.jpg from the bucket
gsutil rm gs://${GOOGLE_CLOUD_PROJECT}/cat.jpg
#Removing gs://nice-beanbag-288720/cat.jpg...
#AccessDeniedException: 403 my-svc-account@nice-beanbag-288720.iam.gserviceaccount.com does not have storage.objects.delete access to the Google Cloud Storage object.

# try deleting the object as owner - abhi.das2007das@gmail.com
gcloud config set account abhi.das2007das@gmail.com
gsutil rm -f gs://${GOOGLE_CLOUD_PROJECT}/cat.jpg
#AccessDeniedException: 403 Object 'nice-beanbag-288720/cat.jpg' is subject to bucket's retention policy and cannot be deleted, overwritten or archived until 2020-09-14T01:52:06.803296431-07:00
# Note: the error message is not same, owner was not able to delete as retention policy is set on the object, hence cant be deleted.
```
