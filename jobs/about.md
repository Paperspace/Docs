# Overview

{% hint style="warning" %}
Jobs have been replaced by a more general framework called Workflows. For the latest info go to [Workflows](https://docs.paperspace.com/gradient/explore-train-deploy/workflows).
{% endhint %}

Gradient Jobs execute generic tasks on remote infrastructure and can be used to perform a variety of functions from compiling a model to running an ETL operation. When you run an Experiment within Gradient, a job is created and executed \(or multiple jobs in the case of distributed training or a hyperparameter sweep\).

Gradient Jobs can be created using the Web UI or via the CLI, and they form part of a larger suite of tools that work seamlessly with Gradient Notebooks and other features of the Gradient platform.

![Jobs are available within a project](../.gitbook/assets/screen-shot-2021-01-18-at-9.56.58-pm.png)

### A Job consists of:

1. a collection of files \(code, resources, etc\) from your local computer or GitHub
2. a container \(with code dependencies and packages pre-installed\)
3. a command to execute \(i.e. `python main.py` or `nvidia-smi`\)

## Running a Job in Gradient

There are several ways to run a Job in Gradient: You can use the [Job Builder](about.md), a web interface for submitting Jobs, the [Gradient CLI](../get-started/install-the-cli.md), or you can clone a public Job.

### Optional Job features

There are many features you will want to check out like outputting your model to the `/artifacts` directory, the persistent data layer at `/storage`, graphing with [Job Metrics](create-a-job/job-metrics/), sharing Jobs with the [public Jobs](create-a-job/public-jobs.md) feature, and more.

## Storage

Jobs have access to your persistent storage \(`/storage`\) and can output files to /artifacts. Learn more about Gradient storage [here](../data/storage/).

## Instance Types

Jobs can be chosen to run on a variety of hardware. Pricing and details for all available options can be found [here](https://gradient.paperspace.com/instances).

