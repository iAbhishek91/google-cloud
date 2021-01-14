# Cloud functions (serverless logic)

- Scenario: There are application which depends on events. For example: There is a function which helps user to uploads images, once the image is uploaded it should be processed in various ways.

Traditionally we can keep both the function in same code base for uploading and processing. Now we need to manage resources as processing images generally takes more resources. So to cut down the maintenance cost we can separate out the processing to cloud functions.

Just let cloud function take care of the function and execute when the event occurs. The Infra side of the problem is taken care by Google.

We just need to pay when the function runs in 100milliseconds intervals. No other cost involved.

Trigger point ranges from varieties of options, like events on **cloud storage**, **cloud pub/sub** or an **http calls**.

Cloud functions are written **in Javascript, managed in NodeJS** environments on GCP. Currently it supports Python 3, and Go as well.

The function have well defined entry point and exit points.

Microservices can be entirely implemented in cloud functions.

Can scale down to zero to planet-scale based on use.

## Use cases

Event driver applications or micro-services.
