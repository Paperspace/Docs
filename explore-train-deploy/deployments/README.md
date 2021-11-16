---
description: Gradient Deployments helps you perform effortless model serving.
---

# Deployments (Preview)

After Notebooks and Workflows, the other major component of Gradient's end-to-end data science platform is Deployments.

A Deployment is used to run container images and to serve your machine learning models using a high-performance, low-latency micro-service with a RESTful API. This allows the model to be run on new unseen data in production, also known as model inference.

![](<../../.gitbook/assets/screen-shot-2021-09-21-at-1.52.29-pm (1).png>)

## Key concepts

Deployments has a number of concepts to allow different configuration.

#### Deployment Spec

A deployment spec is used to represent the desired state of your deployment. With the [Gradient CLI](../../get-started/quick-start/install-the-cli.md) you can use a [YAML file ](../deployments-preview/deployment-spec.md)to change the desired state of your deployment.

#### Deployment Run

A deployment can have multiple runs at the same time. Any update to the deployment spec can create a new deployment run. Once the latest deployment run is ready, the previous deployment run will scale down.

