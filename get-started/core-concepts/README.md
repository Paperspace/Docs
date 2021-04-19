# Core Concepts

## Notebooks

Launch a Jupyter Notebook that includes all the frameworks, libraries, and drivers you need for machine learning. Gradient [Notebooks](../../notebooks/about/) make it easy to explore data and coding concepts and collaborate with other people on projects. 

* No configuration required
* Free access to CPU and GPU instances
* Easy sharing

{% hint style="success" %}
Check out the [FREE GPU](../../instance-types/free-instances.md) option when launching Notebooks!
{% endhint %}

## Projects

{% hint style="warning" %}
Using advanced ML components contained within Projects requires [creating a cluster](../../gradient-private-cloud/about/setup/managed-installation.md).   
{% endhint %}

A Gradient [Project](../about-projects/) is a collection of Workflows, Models, and Deployments. Workflows provide a pipelining capability to automate these components. 

### Workflows \(Private Beta\)

Workflows are the newest and most powerful way to orchestrate full end-to-end machine learning application development.  

### Models

You can either upload a model or generate models from experiments which can be interpreted and stored in the [Gradient Model Repository](../../models/about/).  

### Deployments \(inference/model serving\)

Once a model is created, you can easily serve the model high-performance, low-latency micro-service with a RESTful API. Learn more [here](../../deployments/about.md).

## Data

#### \*\*\*\*[**Versioned Datasets**](../../data/private-datasets-repository/)\*\*\*\*

Datasets have immutable versions that can be used to track your data as it changes. Datasets can be used as input to Gradient workloads as well as outputs. Gradient provides the ability to mount S3 compatible object storage buckets at runtime.  Learn more [here](../../data/private-datasets-repository/).

#### [Persistent Storage](../../data/storage/#persistent-storage) \(legacy\)

Persistent storage is a persistent filesystem automatically mounted on every Notebook and is ideal for storing data like images, datasets, model checkpoints, and more. Learn more [here](../../data/storage/#persistent-storage).

