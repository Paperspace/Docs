---
description: Gradient Deployments helps you perform effortless model serving.
---

# Deployments \(Preview\)

![](../../.gitbook/assets/screen-shot-2021-09-21-at-1.52.29-pm%20%281%29.png)

## Key concepts

A deployment is used to run container images and used to serve your models. Deployments has a number of concepts to allow different configuration.

#### Deployment Spec

A deployment spec is used to represent the desired state of your deployment. With the [Gradient CLI](../../get-started/quick-start/install-the-cli.md) you can use a [yaml file ](deployment-spec.md)to change the desired state of your deployment.

#### Deployment Run

A deployment can have multiple runs at the same time. Any update to the deployment spec can create a new deployment run. Once the latest deployment run is ready, the previous deployment run will scale down.



