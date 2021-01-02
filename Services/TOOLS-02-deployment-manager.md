
# Deploying manager

Its like ansible or chef or terraform. The allow you to automate the infrastructure, repetitive task in GCP.

Deployment manager helps you to create template of the task that you perform.

It helps you to repeatable deployments. This is a declarative approach than imperative approach using GCP SDK.

User need to create YAML/python template describing your environment and use *deployment manager* to create resources.

**Pro tip**: you may choose to version control the deployment manager's templates in cloud-source-repository.

Additionally there are rich set of templates available on marketplace which can used directly. Refer: 06-jenkins-marketplace exercise.

>NOTE: when we launch a template from marketplace deployment manager deploys that template in a compute engine including other resource defined in the template like persistent disk. Its very similar how GKE provision compute engine which runs the k8s workloads.

## features

- declarative
- parallel
- template driven
- jinja templates(same as helm) and python are allowed

## Jinja template

- three parameter are mandatory
  - name
  - type
  - properties

### template example

```yaml
firewall.jinja
resources:
- name: {{ env["name"] }}
  type: compute.v1.firewall #fetch using: gcloud deployment-manager types list | grep firewall
  properties:
    network: {{ properties["network"] }}
    sourceRange: [0.0.0.0/0]
    allowed:
    - IPProtocol: {{ properties["IPProtocol"] }}
      ports: {{ properties["Port"] }}

autonetwork.jinja
resources:
- name: {{ env["name"] }}
  type: compute.v1.network #fetch using: gcloud deployment-manager types list | grep network
  properties:
    autoCreateSubnetworks: true
```

### Call the template

```yaml
config.yaml
imports:
- path: firewall.jinja
- path: autonetwork.jinja

resources:
- name: mynetwork
  type: autonetwork.jinja

- name: ${ref.mynetwork.selfLink} # this makes sure that network is created before firewall rule
  type: firewall.jinja
  properties:
    network: my-network
    IPProtocol: TCP
    Port: [80]
```

## Why not automate using API and SDK ourself

To write an application to automated GCP(or any cloud) using our code is easy but there are maintenance challenges.

- To debug, if something goes wrong, we need to find out which API call failed and where that call is located.
- API changes rapidly and new versions are released, to consume new feature we need to upgrade the code.

Thats the main reason of existence of terraform. in GCP we have deployment manager, it abstract the actual API and hence we don't have to bother about writing codes.

> NOTE: For more advance you can go to market place and look at code other engineers have defined.
