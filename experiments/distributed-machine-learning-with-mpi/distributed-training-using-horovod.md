---
description: >-
  Horovod is an open source framework for distributed deep learning. It is
  available for use with TensorFlow and several other deep learning frameworks
---

# Distributed Training using Horovod

## Horovod Architecture

Horovod’s cluster architecture differs from the parameter server architecture. Horovod uses Ring-AllReduce, where the amount of data sent is more nearly proportional to the number of cluster nodes, which can be more efficient when training with a cluster where each node has multiple GPUs \(and thus multiple worker processes\).

Additionally, whereas the parameter server update process described above is asynchronous, in Horovod updates are synchronous. After all processes have completed their calculations for the current batch, gradients calculated by each process circulate around the ring until every process has a complete set of gradients for the batch from all processes.

At that time, each process updates its local model weights, so every process has the same model weights before starting work on the next batch. The following diagram shows how Ring-AllReduce works \(from [Meet Horovod: Uber’s Open Source Distributed Deep Learning Framework for TensorFlow](https://eng.uber.com/horovod/)\):

![](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2019/08/28/distributed-tensorflow-sagemaker-2.gif)

## MPI 

Horovod employs Message Passing Interface \(MPI\), a popular standard for managing communication between nodes in a high-performance cluster, and uses NVIDIA’s NCCL library for GPU-level communication.

## Usage

The Horovod framework eliminates many of the difficulties of Ring-AllReduce cluster setup and works with several popular deep learning frameworks and APIs. For example, if you are using the popular Keras API, you can use either the reference Keras implementation or tf.keras directly with Horovod without converting to an intermediate API such as tf.Estimator.

## mpirun

With Gradient you have full control over mpirun command.

Example `mpirun`

```bash
mpirun --allow-run-as-root -np 2 --hostfile /generated/hostfile python main.py 
```

**Multi-node Distributed:**

The only requirement to run it as a distributed load on multiple nodes \(only for multi node scenario\) is to pass:

```bash
--hostfile /generated/hostfile
```

## Creating a multi-node experiment using the CLI

The following command creates and starts a multi-node mpi based experiment within the Gradient Project specified with the `--projectId` option.  

```bash
gradient experiments create multinode \
--name distributed-horovod \
--projectId xxxxxxx \
--clusterId xxxxxxx \
--experimentType MPI \
--workerContainer horovod/horovod:0.18.1-tf1.14.0-torch1.2.0-mxnet1.5.0-py3.6 \
--workerMachineType p3.2xlarge \
--workerCommand "sleep infinity" \
--workerCount 2 \
--masterContainer horovod/horovod:0.18.1-tf1.14.0-torch1.2.0-mxnet1.5.0-py3.6 \
--masterMachineType p3.2xlarge \
--masterCommand "mpirun --allow-run-as-root --hostfile /generated/hostfile -bind-to none -map-by slot -mca pml ob1 -mca btl ^openib python main.py"  \
--masterCount 1 \
--workspaceUrl https://github.com/Paperspace/horovod-distributed-example.git \
--apiKey XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX \
--vpc
```

### More info

Horovod's GitHub [repo](https://github.com/uber/horovod/blob/master/docs/running.md) has good explanation of the -mca params. They also have good set of [examples](https://github.com/uber/horovod/tree/master/examples).

