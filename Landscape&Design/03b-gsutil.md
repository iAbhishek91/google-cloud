# gsutil

```sh
# create a bucket in multi region storage class
# Since project id are also unique, we can use that to create the bucket as that also need to be same.
gsutil mb  -l US gs://$DEVSHELL_PROJECT_ID

# copy data from one bucket to compute-engine.
gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png

## verify that the image are there in current directory
ls

# upload to my-own cloud storage
gsutil cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

# copy file from first bucket into the second bucket
gsutil cp gs://$MY_BUKET_NAME_1/cat.jpg gs://$MY_BUCKET_NAME_2/cat.jpg

## verify that the image in the bucket
gsutil ls gs://$MY_BUCKET_NAME_2

# Setting access control on storage

## view access control list before applying any change
gsutil acl get gs://$MY_BUCKET_NAME_1/cat.png

## Set the cloud storage with private access(only owner will have access)
gsutil acl set private gs://$MY_BUCKET_NAME_1/cat.jpg

## validate the access control kist
gsutil acl get gs://$MY_BUCKET_NAME_1/cat.png

## Set cloud storage bucket readable by everyone including unauthenticated users.
## NOTE: this is recommended auth settings of a public hosting website content in cloud storage.
gsutil iam ch allUsers:objectViewer gs://$MY_BUCKET_NAME_1
```
