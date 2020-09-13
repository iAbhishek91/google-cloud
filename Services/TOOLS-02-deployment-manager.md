
# Deploying manager

Its like ansible or chef or terafrom. The allow you to automate the repetitive task in GCP.

Deployment manager helps you to create template of the task that you perform.

It helps you to repeatable deployments. This is a declarative approach than imperative approach using GCP SDK.

User need to create YAML/python template describing your environment and use deployment manager to create resources.

Pro tip: you may choose to version control the deployment manager's templates in cloud-source-repository.

Additionally there are rich set of templates available on marketplace which can used directly. Refer: 06-jenkins-marketplace exercise.

>NOTE: when we launch a template from marketplace deployment manager deploys that template in a compute engine including other resource defined in the template like persistent disk. Its very similar how GKE provision compute engine which runs the k8s workloads.
