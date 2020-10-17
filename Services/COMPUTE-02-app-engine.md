# App Engine (PaaS)

- one of the oldest services created by GCP.
- Its a platform as a service offering of GCP. unlike IaaS (compute engine and kubernetes engine).
- App engine is your best friend if you don't want to focus on Infrastructure.
- Most suited when application architecture is micro-service based.

- **features**
  - App engine does deployments, maintenance, scalability. You just need to focus on application.
  - App engine provides many common services that are required by Application to run. (no-sql database, in-memory caching, load balancing, health checks, logging, and different authentication mechanism).
  - Application code bases are stored in cloud storage.
  - Build and deploy containerized apps(Applications run on docker containers on GCP compute engine VMs) with a click. Each runtime that we specify are maintained run on container. *Details are mentioned on official webpage.*
    - App engine manages these VMs for you and hence its become a PaaS instead of IaaS. User only need to choose the geographical location you want to run. App engine take care of rest of the things.
- **environments**
  - standards and flexible [comparison](https://cloud.google.com/appengine/docs/the-appengine-environments). We may choose both the env simultaneously to take advantage of both.
  - **Standard**
    - Easy deployment of the application.
    - Free daily quota. *Low utilization app may run without any charge*.
    - Usage based pricing. *Pay for what you need and when you need, unlike flexible*.
    - Auto-scale workload. *min zero* Suitable for rapid scaling unlike flexible.
    - Suitable for app which expect sudden and extreme spike in traffic.
    - GCP SDK provides simple app deployment commands.
    - The runtime is provided by Google. The choices are specific version of : Java, Python, PHP , NodeJs, Ruby and Go. *If you want to code on any other language standard environment is not for you. Choose the flexible one.*
    - The standard environment also comes with App engine APIs.
    - They also have some restriction as the code runs on an env called as **sandbox**. This is software construct which is independent of software, hardware, OS, and runtime. This limitation enables standard env to run in a fine grained way.
      - **Limitation of sandbox** *What is sandbox?* refer at bottom of the page.
        - specific version of runtime are supported. and runtime cant be modified.
        - No writing to local files, it need to write database instead, if it want to make data persistent. *Currently its allowed for few of the runtime like java and nodeJS, however for python its still not available*
        - All request time out at 60s
        - Limits on third party software and binaries.
        - No support to web socket.
    - **workflow of standard**
      - Develop the application and test the web app locally using App engine SDK.
      - When ready deploy it using App engine SDK to App Engine.
      - App Engine automatically scales & reliable serves your web application.
        - Once deployed, app engine may call variety of services - like no-sql db, memcache, task queue, scheduled tasks, search, logs using dedicated APIs.

  - **Flexible**
    - Use flexible only if standard do not work for you.
    - No sandbox constraints.
    - Can access App Engine resources. *As the app runs in a docker container running on a compute engine*
    - Flexible environment can also access the services that are provided by standard env.
    - **unlike standard**
      - supports any runtime on the infra. and runtime can be modified using dockerfile.
      - cant scale to zero, min one instance is required.
      - supports web socket.
      - Its not suitable for rapid scaling, or inconsistent traffic.

- **Use Cases**
  - Web application and mobile back-ends load is highly variable or unpredictable.

## Quotas

- app engine application can consume resources up to certain quotas.
  - applications daily consumption can be viewed in the google-cloud-console.
  - Different type of quotas available:
    - *Free quotas*: fixed amount of each resources for free, once free quota is exceeded you will be billed.
    - *Daily quotas*: ensures that apps do not over-consumes a resource to the detriment of other apps. (app will throw err if quota is reached.) Daily quotas are refreshed at midnight Pacific time.
    - *Per-minute quotas*: protects your app form consuming all of its resources in very short period of time. IMP NOTE: if app consumes a resource too quickly an depletes a per minute quota, the word "Limited" appears next to quota page in cloud console.
  - auto-replenish of resources based on type of quotas.
  - App Engine will return 403 or 503, this err can be handled by developer.

## Attribute for pricing

### Standard

- **Location**(basically region)
- **Instance Type**(or classes): determines the memory and CPU available. Currently instance classes starts with *F-frontend* (auto scales) and *B-backend*(manual and basic scale).
- **Instance (per hour)**

### Flexible

- **Location**
- **Cores/vCPU**
- **Memory(per hour)**
- **Persistent disk**

## What is sandbox

Sandbox is a security environment, with restricted access to computer resources like network, cpu, ram, disk. Sandbox region are mainly used to test and validate application.
