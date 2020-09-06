# App Engine (PaaS)

- Its a platform as a service offering of GCP. unlike IaaS (compute engine and kubernetes engine).
- App engine is your best friend if you don't want to focus on Infrastructure.

- **features**
  - App engine does deployments, maintenance, scalability. You just need to focus on application.
  - App engine provides many common services that are required by Application to run. (no-sql database, in-memory caching, load balancing, health checks, logging, and different authentication mechanism).
  - Application code bases are stored in cloud storage.
- **environments**
  - standards and flexible
  - **Standard**
    - Standard is the simpler.
    - Easy deployment of the application.
    - Free daily quota.
    - Usage based pricing.
    - Autoscale workload.
    - Low utilization app may run without any charge.
    - GCP SDK provides simple app deployment commands.
    - The runtime is provided by Google. The choices are specific version of : Java, Python, PHP and Go. If you want to code on any other language standard environment is not for you. Choose the flexible one.
    - The standard environment also comes with App engine APIs.
    - They also have some restriction as the code runs on an env called as **sandbox**. This is software construct which is independent of software, hardware, OS, and runtime. This limitation enables standard env to run in a fine grained way.
      - **Limitation of sandbox**
        - No writing to local files, it need to write database instead, if it want to make data persistent.
        - All request time out at 60s
        - Limits on third party software.
    - **workflow of standard**
      - Develop the application and test the web app locally using App engine SDK.
      - When ready deploy it using App engine SDK to App Engine.
      - App Engine automatically scales & reliable serves your web application.
        - Once deployed, app engine may call variety of services - like no-sql db, memcache, task queue, scheduled tasks, search, logs using dedicated APIs.
  - **Flexible**
    - Use flexible only if standard do not work for you.
    - Build and deploy containerized apps(Applications run on docker containers on GCP compute engine VMs) with a click. App engine manages these VMs for you and hence its become a PaaS instead of IaaS. User only need to choose the geographical location you want to run. App engine take care of rest of the things.
    - No sandbox constraints.
    - Can access App Engine resources.
    - Flexible environment can also access the services that are provided by standard env.

- **Use Cases**
  - Web application and mobile backends load is highly variable or unpredictable.
