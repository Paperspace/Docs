---
description: Gradient Notebooks is a web-based Jupyter IDE with free GPUs.
---

# Gradient Notebooks

## Overview

A notebook is an interactive environment for developing and running code. Gradient Notebooks is based on [Jupyter](https://jupyter.org), which is an open source project behind the majority of popular cloud-hosted notebook platforms.

What differentiates a notebook in Gradient is the ability to access fast and inexpensive GPUs and to extend the use of platform well beyond the notebook phase.

## What is a notebook?

A notebook is a web-based Jupyter interactive development environment. Notebooks are often used by data scientists, data analysts, machine learning engineers, and others to explore code and data.&#x20;



## Notebook architecture

Notebooks are Jupyter kernels that are running on a Kubernetes host ...&#x20;



## How to use these docs

List of docs:

1. How to ...
2. How to ...
3. How to ...

## What are the limitations of a notebook? &#x20;





re an interactive environment for developing and running code. Jupyter notebooks (`.ipynb` files) are supported natively.  You can also treat a Notebook as a full IDE and both write and execute code written in other languages such as Python.  You can run Notebook on CPU or GPU instances.&#x20;

![The Notebook interface](../../.gitbook/assets/screen-shot-2021-04-29-at-1.04.16-pm.png)

Within the Notebook, you can store an unlimited number of documents and other files. You can think of a Gradient Notebook as your persistent, on-demand workspace in the cloud.

{% hint style="info" %}
**NEW!**  Visit the new [ML Showcase](https://ml-showcase.paperspace.com) for a list of sample projects you can fork into your own account.
{% endhint %}

## File Storage

Any data stored in `/storage` will be preserved for you across restarts. Persistent storage is backed by a filesystem and is ideal for storing data like images, datasets, model checkpoints, etc.  Learn more about persistent storage [here](../../more/overview/billing-and-subscriptions/notebooks-storage.md).

## Containers

Notebooks run within Docker containers behind the scenes. Gradient includes a handful of pre-built containers and you can easily use a custom container as well.  View the list of pre-built containers [here](create-a-notebook/notebook-containers/).

### Sharing Notebooks

You can easily generate a link to [share your Notebook](create-a-notebook/share-a-notebook.md) with friends and colleagues or the general public. Public Notebooks can be forked by others into their own account. To learn more about how Notebooks work, you can fork a public demo Notebook [here](https://console.paperspace.com/ps-dan/notebook/pr3k0bq87).  The [ML Showcase](https://ml-showcase.paperspace.com) **** includes several working examples of projects you can run with a couple clicks (project [submissions welcome](https://blog.paperspace.com/write-for-paperspace/)!)

## Tutorial

View a quick tutorial on creating a notebook [here](broken-reference).
