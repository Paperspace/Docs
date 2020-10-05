# Core Concepts

## Notebooks

Gradient integrates with Jupyter Notebooks and Jupyter Lab, making it easy to get a coding environment provisioned in seconds.  Gradient [Notebooks](../notebooks/about.md) make it easy to explore data and coding concepts and collaborate with other people on projects. 

{% hint style="success" %}
Check out the [FREE GPU](../instances/free-instances.md) option when launching Notebooks!
{% endhint %}

## Projects

{% hint style="warning" %}
Using advanced ML components contained within Projects requires [creating a cluster](../gradient-private-cloud/setup/managed-installation.md).   
{% endhint %}

A Gradient [Project](../projects/about.md) is a collection of Experiments, Jobs, Models, and Deployments. Projects can be synced with GitHub with [GradientCI](../projects/gradientci-v2/).

## Experiments

[Experiments](../experiments/about.md) are designed for training machine learning models on GPUs \(and other chips\) without managing any infrastructure. Experiments are used to create and start either a single Job or multiple Jobs \(eg for a hyperparameter search or distributed training\).  

Experiments are part of a larger suite of tools that work seamlessly with Gradient Notebooks, Models, and Deployments, which together form a production-ready ML/AI pipeline.

## Jobs

[Jobs](../jobs/about.md) execute generic tasks on remote infrastructure and can be used to perform a variety of functions from compiling a model to running an ETL operation.  Jobs are made up of a collection of code, data, and a container that are packaged together and remotely executed.  

## Data

#### Persistent Storage

Persistent storage is a persistent filesystem automatically mounted on every Experiment, Job, and Notebook and is ideal for storing data like images, datasets, model checkpoints, and more. Learn more [here](../data/storage.md#persistent-storage).

#### Artifact Storage

Artifact storage is collected and made available after the Experiment or Job run in the CLI and web interface. You can download any files that your job has placed in the `/artifacts` directory from the CLI or UI. If you need to get result data from a job run out of Gradient, use the Artifacts directory. Learn more [here](../data/storage.md#artifact-storage).

#### Workspace Storage

The Workspace storage is typically imported from the local directory in which you started your job. The contents of that directory are zipped up and uploaded to the container in which your job runs. The Workspace exists for the duration of the job run.  If you need to push code up to Gradient and run it, using the Workspace storage is the way to do it. Learn more [here](../data/storage.md#workspace-storage).

#### Private Datasets

Gradient provides the ability to mount S3 compatible object storage buckets to an experiment at runtime.  Learn more [here](../data/private-datasets-repository.md).

## Models

You can either upload a model or generate models from experiments which can be interpreted and stored in the [Gradient Model Repository](../models/about.md).  

## Deployments \(inference/model serving\)

Once a model is created, you can easily serve the model high-performance, low-latency micro-service with a RESTful API. Learn more [here](../deployments/about.md).



