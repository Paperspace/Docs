---
description: How to run single-node and multinode experiments
---

# Experiments

## About

Experiments are the new unit of computation in Gradient Projects, intended to be use for intensive computational tasks like neural network training. Gradient supports single-node experiments as well as distributed training through multinode experiments.

## Single Node

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

![](../.gitbook/assets/image%20%287%29.png)

