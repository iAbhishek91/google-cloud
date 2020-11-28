# Learn the below

How to deploy a microservices application on an existing GKE cluster

How to select appropriate SLIs/SLOs for an application

How to implement SLIs using Cloud Monitoring features

How to use Cloud Trace, Cloud Profiler, and Cloud Debugger to identify software issues

## Steps

### STEP-1: Create the GKE cluster

```sh
# env
gcloud config set compute/zone us-west1-b
export PROJECT=$GOOGLE_CLOUD_PROJECT


# create a GKE cluster and verify
gcloud container clusters list
```

### Step-2: Clone and deploy the microservices

```sh
git clone https://github.com/GoogleCloudPlatform/training-data-analyst

ln -s ~/training-data-analyst/blogs/microservices-demo-1 ~/microservices-demo-1

# download and configure skaffold
curl -Lo skaffold https://storage.googleapis.com/skaffold/releases/v0.36.0/skaffold-linux-amd64 && chmod +x skaffold && sudo mv skaffold /usr/local/bin

# deploy the Microservices using skaffold
cd microservices-demo-1
skaffold run

# Verify the deployment
kubectl get pods
```

"It's impossible to manage a service correctly, let alone well, without understanding which behaviors really matter for that service and how to measure and evaluate those behaviors. To this end, we would like to define and deliver a given level of service to our users, whether they use an internal API or a public product.

"We use intuition, experience, and an understanding of what users want to define **service level indicators (SLIs), objectives (SLOs), and agreements (SLAs)**. These measurements describe basic properties of metrics that matter, what values we want those metrics to have, and how we'll react if we can't provide the expected service. Ultimately, choosing appropriate metrics helps to drive the right action if something goes wrong, and also gives an SRE team confidence that a service is healthy.

"An **SLI** *is a service level indicator—a carefully defined quantitative measure of some aspect of the level of service that is provided*.

"Most services consider request **latency** — how long it takes to return a response to a request — as a key SLI. Other common SLIs include the **error rate**, often expressed as a fraction of all requests received, and system throughput, typically measured in requests per second. Another kind of SLI important to SREs is **availability**, or the fraction of the time that a service is usable. It is often defined in terms of the fraction of well-formed requests that succeed. **Durability** — the likelihood that data is be retained over a long period of time — is equally important for data storage systems. The measurements are often aggregated: i.e., raw data is collected over a measurement window and then turned into a rate, average, or percentile."

Now that you have established a basic understanding, define the SLIs and SLOs for your application. Given that the application itself serves end user ecommerce traffic, it's going to be very important that user experience remains constant and that performance is good. Monitor SLIs for request latency, error rate, throughput, and availability.

It's impossible to develop SLIs without understanding how the application is built. Details are in the original repository, but for this lab, it suffices to understand that:

- Users access the application through the Frontend.
- Purchases are handled by CheckoutService.
- CheckoutService depends on CurrencyService to handle conversions.
- Other services such as RecommendationService, ProductCatalogService, and Adservice are used to provide the frontend with content needed to render the page.

> REF: SLI.png

### Step-3: Configuring SLI

Alerts

- **Latency Policy**: The condition lets you know when you're experiencing performance issues that are impacting user experience. As described in the Service Level Indicators and Objectives table above, use the 99th percentile front end latency as the SLI.
- **Frontend Availability**: Start by monitoring the error rate for the frontend service, since that’s where user experience is going to be most directly impacted. As discussed above, you’re going to consider any failures observed to be an SLO violation. Create an alerting policy that triggers an incident if any failures are observed.

