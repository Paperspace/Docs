# Core Concepts

## Notebooks

Launch a Jupyter Notebook that includes all the frameworks, libraries, and drivers you need for machine learning. Gradient [Notebooks](../../explore-train-deploy/notebooks/) make it easy to explore data and coding concepts, experiment with machine learning models, and collaborate with other people on projects. 

* No configuration required
* Free access to CPU and GPU instances
* Easy sharing

{% hint style="success" %}
Check out the [FREE GPU](../../more/instance-types/free-instances.md) option when launching Notebooks!
{% endhint %}

## Projects

A Gradient [Project](../managing-projects/) is a collection of Workflows, Models, and Deployments. It provides a way to organize your Gradient workload into related groups for manitenance and sharing within a team.

### Workflows

Workflows are the newest and most powerful way to orchestrate full end-to-end machine learning application development. Workflows let you use a [GitHub-action](https://docs.github.com/en/actions) style syntax to easily create powerful automation.

### Models

You can either upload a model or generate models from your training workloads which can be stored in the [Gradient Model Repository](../../data/models/).  

### Deployments \(inference/model serving\)

Once a model is created, you can easily serve the model high-performance, low-latency micro-service with a RESTful API. Learn more [here](../../explore-train-deploy/deployments/).

## Data

#### [**Versioned Datasets**](../../data/data-overview/private-datasets-repository/)

Versioned Datasets are used to manage the flow of data with your machine learning workloads. Datasets have immutable versions that can be used to track your data as it changes. Datasets can be used as input to Gradient workloads as well as outputs. Gradient provides the ability to mount S3 compatible object storage buckets at runtime.  Learn more [here](../../data/data-overview/private-datasets-repository/).

#### [Persistent Storage](../../data/data-overview/#persistent-storage)

Persistent storage is a persistent filesystem automatically mounted on every Notebook and is ideal for storing data like images, datasets, model checkpoints, and more. Gradient Dataset versions are automatically cached to persistent storage for performance.  Learn more [here](../../data/data-overview/#persistent-storage).

