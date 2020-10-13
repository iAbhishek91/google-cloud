# Container Registry

Google container registry are also a public registry, however we can use it from google cloud and apply IAM policy.

Below commands are used to upload images

```sh
# auth to docker registry
gcloud --quiet auth configure-docker

# build and tag the image
run: docker build -t gcr.io/$PROJECT_ID/$IMAGE_NAME:$VERSION .

# push image to gco registry
docker push  gcr.io/$PROJECT_ID/$IMAGE_NAME:$VERSION
```
