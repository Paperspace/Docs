---
description: For multi-node Jobs such as distributed training and hyperparameter tuning.
---

# Overview

Experiments are used to train machine learning models. Gradient supports single-node experiments as well as distributed training through multi-node experiments.  Gradient also supports [Hyperparameter Search](hyperparameters.md).

![](../.gitbook/assets/image%20%2815%29.png)

## Creating Experiments

Experiments can be run from the **Experiment Builder** web interface, our **CLI,** the **GradientCI** bot, or the  **SDK**. Here is a quick overview and instructions for each option:

The **web UI** is great for getting familiar with Experiments and running sample projects.

{% page-ref page="using-experiments/" %}

The **CLI** \(command-line interface\) is the most popular tool for launching Experiments. It's powerful, flexible, and easy-to-use.

{% page-ref page="using-experiments/" %}

The **SDK** let's you programmatically interact with the Gradient platform. The SDK can be incorporated into any python project and enables more advanced ML pipelines.

{% page-ref page="../projects/gradientci.md" %}

**GradientCI** enables you to submit Experiments directly from a GitHub commit \(or branch\). You can launch Experiments without ever leaving your code.

{% page-ref page="../gradient-python-sdk/gradient-python-sdk/" %}

## Experiment Modes

### Single-node

In your your CLI command or`config.yaml`, specify the experiment type as `singlenode`

### Multi-node

Gradient supports both gRPC and MPI protocols for distributed TensorFlow model training. In your CLI command or`config.yaml`, specify the experiment type as either `multinode.` The two types are:

```text
type: "multi-grpc"
```

or

```text
type: "multi-mpi"
```

### Hyperparamater Tuning

See this [article](hyperparameters.md) for more info.

## Storage

#### Persistent Storage

Persistent storage is a persistent filesystem automatically mounted on every Experiment, Job, and Notebook and is ideal for storing data like images, datasets, model checkpoints, and more. Learn more [here](../data/storage.md#persistent-storage).

#### Artifact Storage

Artifact storage is collected and made available after the Experiment or Job run in the CLI and web interface. You can download any files that your job has placed in the `/artifacts` directory from the CLI or UI. If you need to get result data from a job run out of Gradient, use the Artifacts directory. Learn more [here](../data/storage.md#artifact-storage).

#### Workspace Storage

The Workspace storage is typically imported from the local directory in which you started your job. The contents of that directory are zipped up and uploaded to the container in which your job runs. The Workspace exists for the duration of the job run.  If you need to push code up to Gradient and run it, using the Workspace storage is the way to do it. Learn more [here](../data/storage.md#workspace-storage).

#### Private Datasets

Gradient provides the ability to mount S3 compatible object storage buckets to an experiment at runtime.  Learn more [here](../data/private-datasets-repository.md).

{% page-ref page="../data/private-datasets-repository.md" %}

## **Optional Experiment features**

There are many features you will want to check out like outputting your [models](../models/create-a-model/model-path.md), the [persistent data layer](../data/storage.md#persistent-storage) at `/storage`, graphing with [Experiment Metrics](using-experiments/experiment-metrics/), sharing underling Jobs with the [Public Jobs](https://github.com/dkobran/Docs/blob/master/jobs/public-jobs.md) feature, sourcing your code from [private GitHub repositories](using-experiments/experiment-options.md), and [opening ports](using-experiments/ports.md).

## Instance Types

Jobs can be chosen to run on a variety of hardware. Pricing and details for all available options can be found [here](https://gradient.paperspace.com/instances).

## State Transitions

An experiment goes through a number of "states" between being submitted to Gradient \(through the CLI, SDK, the GradientCI GitHub App, or Job Builder Web UI\). These states are enumerated below:

| State | Name |
| :--- | :--- |
| `EXPERIMENT_STATE_CREATED` | Created |
| `EXPERIMENT_STATE_PENDING` | Pending |
| `EXPERIMENT_STATE_PROVISIONING` | Provisioning |
| `EXPERIMENT_STATE_PROVISIONED` | Provisioned |
| `EXPERIMENT_STATE_NETWORK_SETUP` | Network Setup |
| `EXPERIMENT_STATE_RUNNING` | Running |
| `EXPERIMENT_STATE_NETWORK_TEARDOWN` | Network Teardown |
| `EXPERIMENT_STATE_STOPPED` | Stopped \(aka Success\) |
| `EXPERIMENT_STATE_FAILED` | Failed |
| `EXPERIMENT_STATE_CANCELLED` | Cancelled |
| `EXPERIMENT_STATE_ERROR` | Error |

![](../.gitbook/assets/image%20%2859%29.png)
