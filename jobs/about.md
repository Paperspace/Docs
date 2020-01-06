# Overview

Gradient Jobs execute generic tasks on remote infrastructure and can be used to perform a variety of functions from compiling a model to running an ETL operation.  When you run an Experiment within Gradient, a job is created and executed \(or multiple jobs in the case of distributed training or hyperparameter sweeps\).     

Gradient Jobs can be created using the Web UI or via the CLI, and they form part of a larger suite of tools that work seamlessly with Gradient Notebooks and other features of the Gradient platform.  

![Gradient Job Runner in the Web UI](https://support.paperspace.com/hc/article_attachments/360008627173/mceclip1.png)

#### A Job consists of:

1. a collection of files \(code, resources, etc\) from your local computer or GitHub
2. a container \(with code dependencies and packages pre-installed\)
3. a command to execute \(i.e. python main.py or nvidia-smi\)

## Running a Job in Gradient

There are several ways to run a Job in Gradient: You can use the [Job Builder](), a web interface for submitting Jobs, the [Gradient CLI](../get-started/install-the-cli.md), or you can clone a Public Job. 

#### Optional Job features

There are many features you will want to check out like outputting your model to the `/artifacts` directory, the persistent data layer at `/storage`, graphing with [Job Metrics](create-a-job/job-metrics/), sharing Jobs with the [Public Jobs](public-jobs.md) feature, and [opening ports](https://support.paperspace.com/hc/en-us/articles/360003412574-Public-IPs-and-Port-Forwarding) eg for accessing TensorBoard.

## Storage 

Jobs have access to your persistent storage \(`/storage`\) and can output files to /artifacts.  Learn more about Gradient storage [here](../gradient-private-cloud/gradient-node/storage.md).

## Instance Types

Jobs can be chosen to run on a variety of hardware. Pricing and details for all available options can be found [here](https://gradient.paperspace.com/instances).

