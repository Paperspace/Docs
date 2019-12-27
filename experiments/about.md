---
description: For multi-node Jobs such as distributed training and hyperparameter tuning.
---

# About

Experiments are intended to be used for intensive computational tasks like neural network training. Gradient supports single-node experiments as well as distributed training through multinode experiments.

Experiments can be run from the **Experiment Builder** web interface, our **CLI,** the **GradientCI** bot, or our new **SDK**. Here is a quick overview and instructions for each option:

The web interface is great for getting familiar with Experiments and running sample projects.  

{% page-ref page="run-experiments-ui.md" %}

The CLI \(command-line interface\) is the most popular tool for launching Experiments. It's powerful, flexible, and easy-to-use. 

{% page-ref page="run-experiments-cli.md" %}

The SDK let's you programmatically interact with the Gradient platform.  The SDK can be incorporated into any python project and enables more advanced ML pipelines.

{% page-ref page="../projects/gradientci.md" %}

GradientCI enables you to submit Experiments directly from a GitHub commit \(or branch\).  You can launch Experiments without ever leaving your code. 

{% page-ref page="../gradient-python-sdk/gradient-python-sdk/" %}

## Experiment Types

### Single Node

In your your CLI command or`config.yaml`, specify the experiment type as `singlenode`

### Multinode

Gradient supports both gRPC and MPI protocols for distributed TensorFlow model training. In your CLI command or`config.yaml`, specify the experiment type as either `multinode.` The two types are:

```text
type: "multi-grpc"
```

or

```text
type: "multi-mpi"
```

## State Transitions

An experiment goes through a number of "states" between being submitted to Gradient \(through the CLI, SDK, the GradientCI GitHub App, or Job Builder GUI\). These states are enumerated below:

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

![](../.gitbook/assets/image%20%2833%29.png)


## Private Datasets

You may mount private datasets hosted in S3 buckets into experiment environment.

{% page-ref page="datasets.md" %}
