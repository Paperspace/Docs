# Table of contents

* [About Paperspace Gradient](README.md)

## Get Started

* [Quick Start](get-started/quick-start.md)
* [Core Concepts](get-started/core-concepts.md)
* [Install the Gradient CLI](get-started/install-the-cli.md)

## Tutorials

* [Getting Started with Notebooks](tutorials/getting-started-with-gradient-notebooks.md)
* [Train a Model with the Web UI](tutorials/train-a-model-with-the-ui.md)
* [Train a Model with the CLI](tutorials/train-a-model-with-the-cli.md)
* [Registering Models in Gradient](tutorials/registering-models-in-gradient.md)
* [Using Gradient Deployments](tutorials/dealing-with-gradient-deployments.md)
* [Using Custom Containers](tutorials/using-custom-containers-with-gradient.md)

## Notebooks

* [Overview](notebooks/about.md)
* [Using Notebooks](notebooks/create-a-notebook/README.md)
  * [Start a Notebook](notebooks/create-a-notebook/start-a-notebook.md)
  * [Stop a Notebook](notebooks/create-a-notebook/stop-a-notebook.md)
  * [Delete a Notebook](notebooks/create-a-notebook/delete-a-notebook.md)
  * [Rename a Notebook](notebooks/create-a-notebook/rename-a-notebook.md)
  * [Share a Notebook](notebooks/create-a-notebook/share-a-notebook.md)
  * [Fork a Notebook](notebooks/create-a-notebook/fork-a-notebook.md)
  * [Using Notebooks in the CLI](notebooks/create-a-notebook/using-notebooks-in-the-cli.md)
* [Notebook Containers](notebooks/notebook-containers/README.md)
  * [Building a Custom Container](notebooks/notebook-containers/building-a-custom-container.md)
* [Community \(Public\) Notebooks](notebooks/public-notebooks.md)

## Projects

* [Overview](projects/about.md)
* [Managing Projects](projects/managing-projects.md)
* [Deleting a Project](projects/deleting-a-project.md)
* [GradientCI](projects/gradientci.md)

## Experiments

* [Overview](experiments/about.md)
* [Using Experiments](experiments/using-experiments/README.md)
  * [Experiment options](experiments/using-experiments/experiment-options.md)
  * [Single-node & multi-node CLI options](experiments/using-experiments/single-node-and-multi-node-cli-options.md)
  * [Gradient Config File](experiments/using-experiments/gradient-config.yaml.md)
  * [Environment Variables](experiments/using-experiments/environment-variables.md)
  * [Git Commit Tracking](experiments/using-experiments/git-commit-tracking.md)
  * [Experiment Metrics](experiments/using-experiments/experiment-metrics/README.md)
    * [System Metrics](experiments/using-experiments/experiment-metrics/system-metrics.md)
    * [Custom Metrics](experiments/using-experiments/experiment-metrics/custom-metrics.md)
  * [Experiment Logs](experiments/using-experiments/experiment-logs.md)
  * [Experiment Ports](experiments/using-experiments/ports.md)
* [Distributed Training](experiments/distributed-training/README.md)
  * [Distributed Machine Learning with Tensorflow](experiments/distributed-training/multi-node-training.md)
  * [Distributed Machine Learning with MPI](experiments/distributed-training/distributed-machine-learning-with-mpi/README.md)
    * [Distributed Training using Horovod](experiments/distributed-training/distributed-machine-learning-with-mpi/distributed-training-using-horovod.md)
    * [Distributed Training Using ChainerMN](experiments/distributed-training/distributed-machine-learning-with-mpi/distributed-training-using-chainermn.md)
* [Hyperparameter Tuning](experiments/hyperparameters.md)
* [Containers: Public & Private](experiments/containers-public-and-private.md)

## Jobs

* [Overview](jobs/about.md)
* [Using Jobs](jobs/create-a-job/README.md)
  * [Stop a Job](jobs/create-a-job/stop-a-job.md)
  * [Delete a Job](jobs/create-a-job/delete-a-job.md)
  * [List Jobs](jobs/create-a-job/list-your-jobs.md)
  * [Job Logs](jobs/create-a-job/job-logs.md)
  * [Ports](jobs/create-a-job/ports.md)
  * [Job Metrics](jobs/create-a-job/job-metrics/README.md)
    * [System Metrics](jobs/create-a-job/job-metrics/system-metrics.md)
    * [Custom Metrics](jobs/create-a-job/job-metrics/custom-metrics.md)
  * [Job Artifacts](jobs/create-a-job/job-artifacts.md)
* [Public Jobs](jobs/public-jobs.md)

## Models

* [Overview](models/about.md)
* [Create a Model](models/create-a-model.md)
* [Model Path, Parameters, & Metadata](models/model-path.md)
* [Example: Prepare a TensorFlow Model for Deployments](models/preparing-model-for-deployment.md)
* [Managing Models](models/managing-models.md)
* [Public Models](models/public-models.md)

## Deployments

* [Overview](deployments/about.md)
* [Managing Deployments](deployments/managing-deployments/README.md)
  * [Deployment States](deployments/managing-deployments/deployment-states.md)
  * [Optimize Models for Inference](deployments/managing-deployments/optimizing-tensorflow-models-for-inference.md)
  * [A Deployed Model's RESTful API](deployments/managing-deployments/deployment-restful-api.md)

## Data

* [Types of Storage](data/storage.md)
* [Private Datasets](data/private-datasets-repository.md)
* [Managing Data in Gradient](data/managing-data-in-gradient/README.md)
  * [Managing Persistent Storage with VMs](data/managing-data-in-gradient/managing-persistent-storage-with-vms.md)
* [Public Datasets Repository](data/public-datasets-repository.md)

## TensorBoards

* [Overview](tensorboards/about.md)
* [Using TensorBoards](tensorboards/using-tensorboards/README.md)
  * [TensorBoards via TensorFlow Scripting](tensorboards/using-tensorboards/getting-started-with-tensorboards.md)

## Gradient SDK <a id="gradient-python-sdk"></a>

* [Gradient SDK](gradient-python-sdk/gradient-python-sdk/README.md)
  * [Projects Client](gradient-python-sdk/gradient-python-sdk/projects-client.md)
  * [Experiments Client](gradient-python-sdk/gradient-python-sdk/experiments-client.md)
  * [Models Client](gradient-python-sdk/gradient-python-sdk/models-client.md)
  * [Deployments Client](gradient-python-sdk/gradient-python-sdk/deployments-client.md)
  * [Jobs Client](gradient-python-sdk/gradient-python-sdk/jobs-client.md)
* [End to end tutorial](gradient-python-sdk/sdk-tutorial.md)
* [Full SDK Reference](https://paperspace.github.io/gradient-cli/gradient.api_sdk.clients.html)

## Machines \(Paperspace CORE\) <a id="machines"></a>

* [Overview](machines/about.md)
* [Using Machines](machines/using-machines/README.md)
  * [Start a Machine](machines/using-machines/start-machine.md)
  * [Stop a Machine](machines/using-machines/stop-machine.md)
  * [Restart a Machine](machines/using-machines/restart-machines.md)
  * [Update a Machine](machines/using-machines/update-machine.md)
  * [List Machines](machines/using-machines/list-machines.md)
  * [Show a Machine](machines/using-machines/show-machine.md)
  * [Wait For a Machine](machines/using-machines/wait-for-the-machine.md)
  * [Check a Machine's utilization](machines/using-machines/machine-utilization.md)
* [Destroy a Machine](machines/destroy-machine.md)
* [Check availability](machines/check-machine-availability.md)

## Instances

* [Instance Types](instances/instance-types.md)
* [Free Instances \(Free Tier\)](instances/free-instances.md)
* [Instance Tiers](instances/instance-tiers.md)
* [Preemptible Instances](instances/preemptible-instances.md)

## Gradient Private Cloud

* [About](gradient-private-cloud/about.md)
* [Setup](gradient-private-cloud/setup.md)
* [Usage](gradient-private-cloud/usage.md)
* [Gradient Node](gradient-private-cloud/gradient-node/README.md)
  * [Requirements](gradient-private-cloud/gradient-node/requirements.md)
  * [Setup](gradient-private-cloud/gradient-node/setup.md)
  * [Usage](gradient-private-cloud/gradient-node/usage.md)
  * [Node Attributes](gradient-private-cloud/gradient-node/job-scheduling-and-node-attributes.md)
  * [Storage](gradient-private-cloud/gradient-node/storage.md)
  * [Gradient AMI](gradient-private-cloud/gradient-node/gradient-ami.md)

## Public Profiles

* [Public Profiles](public-profiles/gradient-public-profiles.md)

## Release Notes

* [Product release notes](https://updates.paperspace.com/)
* [CLI/SDK Release notes](https://github.com/Paperspace/gradient-cli/releases)

