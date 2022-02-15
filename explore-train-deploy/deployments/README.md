---
description: Gradient Deployments helps you perform effortless model serving.
---

# Gradient Deployments

{% hint style="info" %}
Gradient Deployments is currently in **Preview**. If you would like to provide feedback on the deployments product, please [reach out](https://support.paperspace.com/hc/en-us/requests/new).&#x20;
{% endhint %}

## Overview

After Notebooks and Workflows, the third major component of the Gradient Platform is Deployments.

![Creating a new deployment in the Gradient console.](<../../.gitbook/assets/create-new-deployment (1).gif>)

Deployments is used to run container images and to serve machine learning models using a high-performance, low-latency micro-service with a RESTful API.&#x20;

This allows the model to be run on new unseen data in production, also known as model inference.

![Example deployment with YAML spec.](<../../.gitbook/assets/screen-shot-2021-09-21-at-1.52.29-pm (1).png>)

## Where to start

The best place to start learning how to deploy models on Gradient is the official Gradient Deployments Tutorial:

{% content-ref url="../../get-started/tutorials-list/gradient-deployments-tutorial.md" %}
[gradient-deployments-tutorial.md](../../get-started/tutorials-list/gradient-deployments-tutorial.md)
{% endcontent-ref %}



## Key concepts

Deployments has a number of concepts to allow different configuration.

#### Deployment Spec

A deployment spec is used to represent the desired state of your deployment. With the [Gradient CLI](../../get-started/quick-start/install-the-cli.md) you can use a [YAML file ](../deployments-preview/deployment-spec.md)to change the desired state of your deployment.

#### Deployment Run

A deployment can have multiple runs at the same time. Any update to the deployment spec can create a new deployment run. Once the latest deployment run is ready, the previous deployment run will scale down.

