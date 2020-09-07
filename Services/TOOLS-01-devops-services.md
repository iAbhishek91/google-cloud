# DevOps tools

## Cloud build

- CI CD platform on GCP.
- This is a managed service by google.
- Tight integration with cloud source repo, github and bitbuket.
- Can also be used for building images on cloud. Native support of docker integration with automated deployment to k8s and GKE.
- Scanning of source code for vulnerabilities through efficient OS package scanning.

## Container Registry

- Single location to mange container images and repositories.
- Store images close to GCE, GKE and K8s cluster.
- Secure, private scalable Docker registry with in GCP.
- it uses RBAC to access, view and download images.
- Tightly integrated with IAM.
- Security scanning - Detect vulnerabilities in early stages of the software deployments.
- Lock un secure images: supports auto lock down feature wof vulnerable container images.
- tightly integrated with cloud build, it can trigger build when tag changes.
