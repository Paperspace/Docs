# Core Concepts

{% hint style="warning" %}
This section of the documentation covers our previous generation of Gradient. For the current version go to [Gradient Next](https://docs.paperspace.com/gradient).
{% endhint %}

## Notebooks

Launch a Jupyter Notebook that includes all the frameworks, libraries, and drivers you need for machine learning. Gradient [Notebooks](../notebooks/about.md) make it easy to explore data and coding concepts and collaborate with other people on projects.

* No configuration required
* Free access to CPU and GPU instances
* Easy sharing

{% hint style="success" %}
Check out the [FREE GPU](../instances/instance-types/free-instances.md) option when launching Notebooks!
{% endhint %}

## Projects

A Gradient [Project](../projects/about.md) is a collection of Experiments, Jobs, Models, and Deployments. Workflows provide a pipelining capability to automate these components. Projects can be synced with GitHub with [GradientCI](../projects/gradientci-v2/).

### Workflows

Workflows are the newest and most powerful way to orchestrate full end-to-end machine learning application development. For the latest info go to [Workflows](https://docs.paperspace.com/gradient/explore-train-deploy/workflows).

### Experiments

{% hint style="warning" %}
Experiments have been replaced by a more general framework called Workflows. For the latest info go to [Workflows](https://docs.paperspace.com/gradient/explore-train-deploy/workflows).
{% endhint %}

[Experiments](../experiments/about.md) are designed for training machine learning models on GPUs \(and other chips\) without managing any infrastructure. Experiments are used to create and start either a single Job or multiple Jobs \(eg for a hyperparameter search or distributed training\).

### Jobs

{% hint style="warning" %}
Job have been replaced by a more general framework called Workflows. For the latest info go to [Workflows](https://docs.paperspace.com/gradient/explore-train-deploy/workflows).
{% endhint %}

[Jobs](../jobs/about.md) execute generic tasks on remote infrastructure and can be used to perform a variety of functions from compiling a model to running an ETL operation. Jobs are made up of a collection of code, data, and a container that are packaged together and remotely executed.

### Models

You can either upload a model or generate models from experiments which can be interpreted and stored in the [Gradient Model Repository](../models/about.md).

### Deployments \(inference/model serving\)

Once a model is created, you can easily serve the model high-performance, low-latency micro-service with a RESTful API. Learn more [here](../deployments/about.md).

## Data

#### [**Versioned Datasets**](../data/private-datasets-repository.md)

Versioned Datasets are used to manage the flow of data with your machine learning workloads. Datasets have immutable versions that can be used to track your data as it changes. Dataset version can be used as input to Gradient workloads as well as outputs.

Gradient provides the ability to mount S3 compatible object storage buckets to an experiment at runtime. Learn more [here](../data/private-datasets-repository.md).

#### [Persistent Storage](../data/storage/managing-data-in-gradient/managing-persistent-storage-with-vms.md)

Persistent storage is a persistent filesystem automatically mounted on every Experiment, Job, and Notebook and is ideal for storing data like images, datasets, model checkpoints, and more. Learn more [here](../data/storage/#persistent-storage).

#### [Artifact Storage](../jobs/create-a-job/job-artifacts.md)\*\*\*\*

Artifact storage is collected and made available after the Experiment or Job run in the CLI and web interface. You can download any files that your job has placed in the `/artifacts` directory from the CLI or UI. If you need to get result data from a job run out of Gradient, use the Artifacts directory. Learn more [here](../data/storage/#artifact-storage).

#### [Workspace Storage](../notebooks/create-a-notebook/notebook-include.md)

The Workspace storage is typically imported from the local directory in which you started your job. The contents of that directory are zipped up and uploaded to the container in which your job runs. The Workspace exists for the duration of the job run. If you need to push code up to Gradient and run it, using the Workspace storage is the way to do it. Learn more [here](../data/storage/#workspace-storage).

