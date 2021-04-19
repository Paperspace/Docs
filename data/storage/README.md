---
description: There are two types of storage offered in Gradient
---

# Data Overview

## Datasets

Gradient provides the ability to mount S3 compatible object storage buckets to an experiment at runtime.  Learn more [here](../private-datasets-repository/).

## Persistent Storage

Persistent storage is a high-performance storage directory located at `/storage` where you can read and write files. Persistent storage is backed by a filesystem and is ideal for storing data like images, datasets, model checkpoints etc.  Anything you store in the `/storage` directory will be accessible across multiple runs of Experiments, Jobs and Notebooks in a given storage region. 

Persistent Storage is kept in three regions based on your machine type or tier:

1. PS East Coast \(NY2\)
2. GCP West
3. PS West Coast \(for the [Free Tier](../../instances/instance-types/free-instances.md) on Gradient\)

{% hint style="warning" %}
Persistent Storage is specific to each region. This means that data in your Persistent Storage for the Free Tier is not be accessible from paid instance types, and vice versa.
{% endhint %}

