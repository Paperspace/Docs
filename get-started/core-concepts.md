# Core Concepts

## Projects

A Gradient [Project](../projects/about.md) is a collection of Experiments, Jobs, Artifacts, and Models. Projects can be created manually or automatically from a Job corresponding to the current working directory name.

## Notebooks

![](../.gitbook/assets/image%20%284%29.png)

A [Notebook](../notebooks/about.md) is an interactive coding environment that allows you to mix code or formulas with text and diagrams, visualizations, and other media. Notebooks make it easy to explore data and coding concepts, and collaborate with other people on projects. Gradient integrates with Jupyter Notebooks and Jupyter Lab, making it easy to get a coding environment provisioned in seconds.

## Experiments

[Experiments](../experiments/about.md) are designed for executing code \(such as training a deep neural network\) on a CPU or GPU without managing any infrastructure. Experiments are used to create and start either a single Job or multiple Jobs \(eg for a hyperparameter search or distributed training\).  

Experiments are part of a larger suite of tools that work seamlessly with Gradient Notebooks, and our Core product, which together form a production-ready ML/AI pipeline.

## Jobs

Jobs are a made up of a collection of code, data, and a container that are packaged together and remotely executed.  Jobs are initiated by a command such as`main.py` or `nvidia-smi.`

## Data

#### Persistent Storage

Persistent storage is a persistent filesystem automatically mounted on every Experiment, Job, and Notebook and is ideal for storing data like images, datasets, model checkpoints, and more. Learn more [here](../data/storage.md#persistent-storage).

#### Artifact Storage

Artifact storage is collected and made available after the Experiment or Job run in the CLI and web interface. You can download any files that your job has placed in the `/artifacts` directory from the CLI or UI. If you need to get result data from a job run out of Gradient, use the Artifacts directory. Learn more [here](../data/storage.md#artifact-storage).

#### Workspace Storage

The Workspace storage is typically imported from the local directory in which you started your job. The contents of that directory are zipped up and uploaded to the container in which your job runs. The Workspace exists for the duration of the job run.  If you need to push code up to Gradient and run it, using the Workspace storage is the way to do it. Learn more [here](../data/storage.md#workspace-storage).

## Models

Paperspace experiments can generate machine learning models, which can be interpreted and stored in the [Gradient Model Repository](../models/about.md).  

## Deployments \(inference/model serving\)

Once a model is created, you can easily serve the model high-performance, low-latency micro-service with a RESTful API. Learn more [here](../deployments/about.md).

