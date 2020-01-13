# Distributed Machine Learning with MPI

{% hint style="warning" %}
This feature is currently only available to our Gradient Enterprise Customers. [Contact Sales](https://info.paperspace.com/contact-sales) to learn more. 
{% endhint %}

MPI \(Message Passing Interface\) is the _de facto_ standard distributed communications framework for scientific and commercial parallel distributed computing. 

Paperspace Gradient supports both [Open MPI](https://www.open-mpi.org/) and [Intel MPI ](https://software.intel.com/en-us/mpi-library)implementations.   

```
$ gradient experiments create multinode \
--name mpi-test \
--experimentType MPI 
--workerContainer horovod/horovod:0.18.1-tf1.14.0-torch1.2.0-mxnet1.5.0-py3.6 \
--workerMachineType p2.xlarge \
--workerCount 2 \
--masterContainer horovod/horovod:0.18.1-tf1.14.0-torch1.2.0-mxnet1.5.0-py3.6 \
--masterMachineType p2.xlarge \
--masterCommand "mpirun --allow-run-as-root -np 1 --hostfile /generated/hostfile  -bind-to none -map-by slot  -x NCCL_DEBUG=INFO -mca pml ob1 -mca btl ^openib python examples/keras_mnist.py"  \
--masterCount 1 \
--workspace https://github.com/horovod/horovod.git \
--apiKey XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX \
--vpc
```

## How does MPI work?

The MPI command is executed only on the master worker. Then, the master worker connects to the other workers to spin up processes.

In order for this to work, the master worker requires password-less ssh access to all the workers. There are many resources that describe how to set this up; a simple Google search will show you pages like [this](https://source.ggy.bris.ac.uk/wiki/Configure_ssh_for_MPI). This is not difficult to do, but it takes time to set up.

On Gradient, all of this setup is taken care of for you – all you'll need to do is run an MPI command. Continue reading to learn how!

## Prerequisites

To launch an MPI experiment, all you need is:

* Docker image with MPI library installed
* At Least 2 machines \(1 Master, 1 Worker\)
* Gradient CLI
* A Gradient Enterprise cluster \([contact Sales](https://info.paperspace.com/contact-sales) to get started\)

That's it!

## Security

By default, all inter-node communication is over the SSH layer. Before launching your workload, Gradient will automatically generate new SSH keys, and then will distribute them across all nodes that will be used in the experiment.

## Host File

Gradient will generate a host file with list of available nodes at:

```text
--hostfile /generated/hostfile
```

_Note: when using `mpirun`, be sure to specify the host file._

## mpirun

With Gradient you have full control over mpirun command.

Example `mpirun`

```bash
mpirun --allow-run-as-root -np 2 --hostfile /generated/hostfile python main.py 
```

## Show Me Some Examples!

Now that we have a good foundation of how distributed training and inter-node communication works, let's look at two examples.

For simplicity's sake, we present here two examples \([Horovod](distributed-training-using-horovod.md) and [ChainerMN](distributed-training-using-chainermn.md)\) with relatively simple code, but these examples \(especially Horovod\) should give you a good idea of how to run any MPI jobs on Gradient.





