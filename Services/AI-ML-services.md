# AI an ML services

AI building blocks provide AI through simple REST calls.

## Cloud Machine Learning API

- Provides training models on custom datasets.

## AutoML

- enables training high-quality models specific to a business problem.
- custom machine learning models without writing code.
- AutoML uses google's state-of-the-art machine learning algorithms.
- AutoML provides services for:
  - Sight: Vision and Video
  - Language: Translation and Natural language processing
  - Structured Data: Tabular data

**When to use AutoML instead of AI Building blocks**?

- Building blocks are like black boxes, it cant perform AI on custom datasets. For example when  you send a image of a "dog", to vision API, it returns an JSON payload saying that it is an animal and it is a dog.

However, if the requirement of understand the breed of the dog(one level deeper), building block will not be helpful. In this case you can use AutoML to train using data model and achieve what is required.

## AI building blocks

Best part of these APIs are, without learning the under the hood of ML we can just use the API and benefits from the APIs.

### SIGHT (Vision and Video API)

- Call the API with a Image, the API will return you with the objects found in the image. Or can group images based on certain objects.

### CONVERSATION (Dialogflow, text to speech, speech to text)

- Call the API with a text file, it will return you a audio file. Vice versa.

### LANGUAGE (Natural language processing API and Translation API)

- Call the API with a string written in one language, it will return you a string after translation.

### STRUCTURED DATA (AutoML tables, Recommendations AI, Cloud Inference API)

## Job API

## AI Platform

- Provides entire spectrum of end-to-end ML pipelines on-premises and cloud.
- Built on a open source ML project based on Kubernetes, kubeflow.
- Includes tools for data preparation, training, and inference.
- Its like jenkins pipeline, where tht pipeline are broken into stages, example pipeline are below:
  - Ingest data
  - Prepare
  - Preprocess
  - Discover
  - Develop
  - Train
  - Test and Analyze
  - Deploy

- AI platform gives scalable framework for performing all the AI operations.
- AI platform can be deployed on-premise kubernetes cluster as well. So its not only confined to cloud.
- They can be extended for example, we can to training on premise and the deployment can be done on cloud.

## AI Hub

- Is a Google hosted repository to discover, share and deploy ML models.
- This is one of the recent services added to the portfolio.

- During the development of AI and ML models there are several artifacts that are generated, from data-set, to fully trained models, Juiper notebooks, etc. These artifact can be shared in a collaborative fashion between the teams of data scientists.
- Share private and public content.

- AI hub includes:
  - Kubeflow Pipeline components
  - Jupyter Notebooks
  - Tensor Flow models (for plugin into neural network)
  - VM Images
  - Trained models ( ready for inferencing)
