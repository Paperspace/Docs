# About

The[ Gradient Jobs](https://www.paperspace.com/console/jobs) are designed for executing code \(such as training a deep neural network\) on a cluster of GPUs without managing any infrastructure.

Gradient Jobs part of a larger suite of tools that work seamlessly with Gradient Notebooks.  

![](https://support.paperspace.com/hc/article_attachments/360008627173/mceclip1.png)

#### A Job consists of:

1. a collection of files \(code, resources, etc\) from your local computer or GitHub
2. a container \(with code dependencies and packages pre-installed\)
3. a command to execute \(i.e. python main.py or nvidia-smi\)

## Running a Job in Gradient

There are several ways to run a Job in Gradient: You can use the [Job Builder](../experiments/experiment-builder-interface.md), a web interface for submitting Jobs, the [Paperspace CLI](../cli/install-the-cli.md), or you can clone a Public Job. 

#### Optional Job features

There are many features you will want to check out like outputting your model to the `/artifacts` directory, the persistent data layer at /storage, graphing with [Job Metrics](graphing-custom-metrics/), sharing Jobs with the [Public Jobs](public-jobs.md) feature, and [opening ports](https://support.paperspace.com/hc/en-us/articles/360003412574-Public-IPs-and-Port-Forwarding) eg for accessing TensorBoard.

## Compute Types

Jobs can be chosen to run on a variety of hardware. Pricing and details for all available options can be found [here](https://gradient.paperspace.com/instances).

