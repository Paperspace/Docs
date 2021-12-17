---
description: >-
  Welcome to Gradient Deployments! In this tutorial we'll cover everything you
  need to know to start deploying a model to an endpoint using Gradient.
---

# Gradient Deployments Tutorial

## Introduction

[Gradient Deployments](https://gradient.run/deployments) helps us perform effortless model serving to an API endpoint. During this tutorial we'll learn how to use Gradient to deploy a machine learning model using a high-performance, low-latency microservice with a RESTful API.

![This deployment provides an endpoint to reach a hosted Streamlit application.](<../../.gitbook/assets/image (90) (1) (1).png>)

Gradient Deployments makes it easy to deploy a container image to an API endpoint for hosting or inference.&#x20;

In [Part 1](gradient-deployments-tutorial.md#part-1-deploy-a-simple-streamlit-application) of this tutorial, we're going to deploy a generic version of [Streamlit](https://streamlit.io) to an endpoint.&#x20;

In [Part 2](gradient-deployments-tutorial.md#part-2-deploy-from-gradient-model-registry), we're going to demonstrate end-to-end capabilities by training a simple model with Gradient Workflows and then deploying it as an inference server via Gradient Deployments.&#x20;

Let's get started!

## Part 1: Deploy a simple Streamlit application

In Part 1 of this tutorial, our goal is to deploy an application as fast as possible. Once we get a handle on the look and feel of a deployment, we'll then move on to Part 2 during which we'll train and deploy an inference server capable of responding to a query.&#x20;

In service of our goal of getting something deployed quickly in the first part of this tutorial, we're going to be using the [Streamlit](https://streamlit.io) demo application that is available as a starter deployment within the Gradient console.

Here is what we're going to do:

* Create a new project in Gradient
* Create a Streamlit deployment within this project
* Confirm that our new deployment is online and functional

### Create a project

If we haven't already created a project in the Gradient console, we'll need to do that first. Let's select `Create a Project` in our workspace or else let's select the project that we'd like to use for the tutorial.

Here we've named our new project `Deployments Tutorial` because everything we're going to do in this project is related to this very tutorial.

![If we haven't made a Project yet in Gradient, we'll create a new one now. We're calling our Project Deployments Tutorial.](<../../.gitbook/assets/image (92) (1).png>)

Great! We should now have a new project in Gradient with the name `Deployments Tutorial`.

We can create as many projects as we like -- so feel free to create a new project just to keep things nice and tidy.&#x20;

After we create a new project, we're going to create a new Deployment within that project.

### Create a deployment using a basic template in the console

Let's go ahead and create a deployment within our project. Once we're within the project in the UI (we can confirm this by seeing the name of our project in the top left along with the button to navigate back to `All Projects`) let's tab over to the `Deployments` panel and select `Create`.

Let's name our new deployment `Streamlit deployment` and then press the big button `Create Deployment`.&#x20;

![We create a new deployment and name it Streamlit deployment to make it easy to find later.](<../../.gitbook/assets/image (86).png>)

Excellent! While our deployment is spinning-up, let's take a look at the deployment spec that we just ran:

![Here we're using a simple deployment spec that uses Streamlit.](<../../.gitbook/assets/image (87).png>)

The spec for this deployment looks like this:

```
image: lucone83/streamlit-nginx
port: 8080
env:
  - name: ENV
    value: VAR
resources:
  replicas: 1
  instanceType: C4
```

Let's break down our instructions to Gradient:

* `image` - the [specified image](https://hub.docker.com/r/lucone83/streamlit-nginx) or container for Gradient to pull from DockerHub
* `port` - the communication endpoint that the deployment server should expose to the open internet
* `env` - environment variables to apply at runtime
* `resources` - compute instance to apply to this job

As we can see, there is a good amount of configuration options available. If we wanted to change the instance type, for example, we would simply need to modify the `resources` block. If we wanted to upgrade our processor to a C5 instance, for example, we would write:

```
resources:
  replicas: 1
  instanceType: C5
```

That's all there is to it! For more information on the deployment spec, be sure to [read the docs](https://docs.paperspace.com/gradient/explore-train-deploy/deployments/deployment-spec).&#x20;

Meanwhile, let's see the result of our deployment:

![Loading Streamlit on our Gradient endpoint.](<../../.gitbook/assets/image (91) (1).png>)

Excellent! It takes about 30 seconds for our deployment to come up, but once it does the UI state changes to `Ready` and the link to our Streamlit deployment brings us to a hosted endpoint where we can demo a number of Streamlit features.&#x20;

We've now successfully launched our first deployment!&#x20;

In the next part of the tutorial we'll take a look at doing a more end-to-end Gradient Deployments project where we will actually train a model first and then host it to an endpoint.

## Part 2: Deploy from Gradient model registry

Coming soon!

