# gsutil

```sh
# create a bucket in multi region storage class
# Since project id are also unique, we can use that to create the bucket as that also need to be same.
gsutil mb  -l US gs://$DEVSHELL_PROJECT_ID

# copy data from one bucket to compute-engine.
gsutil cp gs://cloud-training/gcpfi/my-excellent-blog.png my-excellent-blog.png

## verify that the image are there in current directory
ls

## upload to my-own cloud storage
gsutil cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

## verify that the image in the bucket
gsutil ls gs://$DEVSHELL_PROJECT_ID
```
