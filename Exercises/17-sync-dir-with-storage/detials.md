# Sync

```sh
gcloud rsync ./directory gs://name/my-sync-dir
gcloud rsync -r ./directory gs://name/my-sync-dir # recursive
gcloud rsync -r -d ./directory gs://name/my-sync-dir # recursive and delete which are not available in src
```
