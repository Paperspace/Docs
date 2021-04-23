---
description: There are two types of storage offered in Gradient
---

# Data

## Datasets

Gradient provides the ability to mount S3 compatible object storage buckets to workloads at runtime.  Datasets have immutable versions that can be used to track your data as it changes.  Learn more [here](private-datasets-repository/).

## Persistent Storage 

Persistent storage is a high-performance storage directory located at `/storage` within Notebooks where you can read and write files. Persistent storage is backed by a filesystem and is ideal for storing data like images, datasets, model checkpoints etc.  Anything you store in the `/storage` directory will be accessible across multiple runs of Notebooks in a given storage region. 

{% hint style="info" %}
Persistent Storage is specific to each region. 
{% endhint %}

{% hint style="info" %}
Persistent storage is only available in the managed service or private clusters.
{% endhint %}

