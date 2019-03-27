---
description: How to run single-node and multinode experiments
---

# Experiments

## About

Experiments are the new unit of computation in Gradient Projects, intended to be use for intensive computational tasks like neural network training. Gradient supports single-node experiments as well as distributed training through multinode experiments.

## Single Node

In your `config.yaml`, specify the experiment `type` as `single`:

```text
type: "single"
```

## Multinode

Gradient supports both gRPC and MPI protocols for distributed TensorFlow model training. In your `config.yaml`, specify the experiment `type` as either `multi-grpc` or `multi-mpi`:

```text
type: "multi-grpc"
```

or

```text
type: "multi-mpi"
```



### State Transitions

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

![](../.gitbook/assets/statetransition.png)

