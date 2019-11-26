# Table of contents

* [About Paperspace Gradient](README.md)

## Get Started

* [Quick Start](get-started/quick-start.md)
* [Core Concepts](get-started/core-concepts.md)
* [Install the Gradient CLI](get-started/install-the-cli.md)

## Tutorials

* [Getting Started with Notebooks](tutorials/getting-started-with-gradient-notebooks.md)
* [Train & Deploy an ML Model with the Gradient CLI](tutorials/training-and-deploying-an-ml-model-with-gradient-cli.md)
* [Train & Deploy an ML Model with the Experiment Builder](tutorials/training-and-deploying-an-ml-model-with-gradient-ui.md)
* [Registering Models in Gradient](tutorials/registering-models-in-gradient.md)
* [Using Gradient Deployments](tutorials/dealing-with-gradient-deployments.md)
* [Launching Notebooks from Custom Containers](tutorials/using-custom-containers-with-gradient.md)

## Notebooks

* [About](notebooks/about.md)
* [Create a Notebook](notebooks/create-a-notebook.md)
* [Notebook Actions](notebooks/notebook-actions/README.md)
  * [Start a Notebook](notebooks/notebook-actions/start-a-notebook.md)
  * [Stop a Notebook](notebooks/notebook-actions/stop-a-notebook.md)
  * [Fork a Notebook](notebooks/notebook-actions/fork-a-notebook.md)
  * [Share a Notebook](notebooks/notebook-actions/share-a-notebook.md)
  * [Delete a Notebook](notebooks/notebook-actions/delete-a-notebook.md)
  * [Rename a Notebook](notebooks/notebook-actions/rename-a-notebook.md)
* [Notebook Containers](notebooks/notebook-containers/README.md)
  * [Building a Custom Container](notebooks/notebook-containers/building-a-custom-container.md)
* [Community \(Public\) Notebooks](notebooks/public-notebooks.md)

## Public Profiles

* [Public Profiles](public-profiles/gradient-public-profiles.md)

## Projects

* [About](projects/about.md)
* [Create a Project via the UI](projects/create-a-project.md)
* [Create a Project via the CLI](projects/create-a-project-using-cli.md)
* [Deleting a Project](projects/deleting-a-project.md)
* [GradientCI](projects/gradientci.md)

## Experiments

* [About](experiments/about.md)
* [Run Experiments via the UI](experiments/run-experiments-ui.md)
* [Run Experiments via the CLI](experiments/run-experiments-cli.md)
* [Distributed Machine Learning with Tensorflow](experiments/multi-node-training.md)
* [Distributed Machine Learning with MPI](experiments/distributed-machine-learning-with-mpi/README.md)
  * [Distributed Training using Horovod](experiments/distributed-machine-learning-with-mpi/distributed-training-using-horovod.md)
  * [Distributed Training Using ChainerMN](experiments/distributed-machine-learning-with-mpi/distributed-training-using-chainermn.md)
* [Hyperparameter Tuning](experiments/hyperparameters.md)
* [Containers: Public & Private](experiments/containers-public-and-private.md)

## Jobs

* [About](jobs/about.md)
* [Create a Job](jobs/create-a-job.md)
* [Stop a Job](jobs/stop-a-job.md)
* [Delete a Job](jobs/delete-a-job.md)
* [List Jobs](jobs/list-your-jobs.md)
* [Job Logs](jobs/job-logs.md)
* [Job Artifacts](jobs/job-artifacts.md)
* [Job Metrics](jobs/job-metrics/README.md)
  * [System Metrics](jobs/job-metrics/system-metrics.md)
  * [Custom Metrics](jobs/job-metrics/custom-metrics.md)
* [Public Jobs](jobs/public-jobs.md)

## Models

* [About](models/about.md)
* [Create a Model](models/create-a-model.md)
* [Default Model path](models/model-path.md)
* [Import models to Gradient](models/import-your-model-to-gradient.md)

## Deployments

* [About](deployments/about.md)
* [Preparing Model for Deployment](deployments/preparing-model-for-deployment.md)
* [Create a Deployment \(UI\)](deployments/create-a-deployment-ui.md)
* [Create a Deployment \(CLI\)](deployments/create-deployment-cli.md)
* [A Deployed Model's RESTful API](deployments/deployment-restful-api.md)
* [Optimizing Models for Inference](deployments/optimizing-tensorflow-models-for-inference.md)
* [Deployment States](deployments/deployment-states.md)

## TensorBoards

* [About](tensorboards/about.md)

## Machines

* [About](machines/about.md)
* [Create a Machine via the GUI](machines/create-a-machine-via-the-gui.md)
* [Create a Machine via the CLI](machines/create-a-virtual-machine.md)
* [Check a Machine's availability](machines/check-machine-availability.md)
* [Destroy a Machine](machines/destroy-machine.md)
* [List Machines](machines/list-machines.md)
* [Restart a Machine](machines/restart-machines.md)
* [Show a Machine](machines/show-machine.md)
* [Start a Machine](machines/start-machine.md)
* [Stop a Machine](machines/stop-machine.md)
* [Update a Machine](machines/update-machine.md)
* [Check a Machine's utilization](machines/machine-utilization.md)
* [Wait For a Machine](machines/wait-for-the-machine.md)

## Data

* [Types of Storage](data/storage.md)
* [Managing Data in Gradient](data/managing-data-in-gradient.md)
* [Managing Persistent Storage with VMs](data/managing-persistent-storage-with-vms.md)
* [Public Datasets Repository](data/public-datasets-repository.md)

## Instances

* [Instance Types](instances/instance-types.md)
* [Free Instances \(Free Tier\)](instances/free-instances.md)
* [Instance Tiers](instances/instance-tiers.md)
* [Preemptible Instances](instances/preemptible-instances.md)

## Gradient SDK <a id="gradient-python-sdk"></a>

* [Gradient SDK](gradient-python-sdk/gradient-python-sdk/README.md)
  * [Projects Client](gradient-python-sdk/gradient-python-sdk/projects-client.md)
  * [Experiments Client](gradient-python-sdk/gradient-python-sdk/experiments-client.md)
  * [Models Client](gradient-python-sdk/gradient-python-sdk/models-client.md)
  * [Deployments Client](gradient-python-sdk/gradient-python-sdk/deployments-client.md)
  * [Jobs Client](gradient-python-sdk/gradient-python-sdk/jobs-client.md)
* [End to end tutorial](gradient-python-sdk/sdk-tutorial.md)
* [Full SDK Reference](https://paperspace.github.io/gradient-cli/gradient.api_sdk.clients.html)

## Gradient Private Cloud

* [About](gradient-private-cloud/about.md)
* [Requirements](gradient-private-cloud/requirements.md)
* [Setup](gradient-private-cloud/setup.md)
* [Gradient AMI](gradient-private-cloud/gradient-ami.md)
* [Usage](gradient-private-cloud/usage.md)
* [Node Attributes](gradient-private-cloud/job-scheduling-and-node-attributes.md)
* [Storage](gradient-private-cloud/storage.md)

## Release Notes

* [Product release notes](https://support.paperspace.com/hc/en-us/articles/217560197)
* [CLI/SDK Release notes](https://github.com/Paperspace/gradient-cli/releases)

