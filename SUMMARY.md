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
* [Advanced: Distributed training sample project](tutorials/advanced-distributed-training-sample-project.md)
* [Registering Models in Gradient](tutorials/registering-models-in-gradient.md)
* [Using Gradient Deployments](tutorials/dealing-with-gradient-deployments.md)
* [Using Custom Containers](tutorials/using-custom-containers-with-gradient.md)

## Notebooks

* [Overview](notebooks/about.md)
* [Using Notebooks](notebooks/create-a-notebook/README.md)
  * [The Notebook interface](notebooks/create-a-notebook/the-notebook-interface.md)
  * [Notebook metrics](notebooks/create-a-notebook/notebook-metrics.md)
  * [Share a Notebook](notebooks/create-a-notebook/share-a-notebook.md)
  * [Fork a Notebook](notebooks/create-a-notebook/fork-a-notebook.md)
  * [Notebook Directories](notebooks/create-a-notebook/notebooks-directories.md)
* [Notebook Containers](notebooks/notebook-containers/README.md)
  * [Building a Custom Container](notebooks/notebook-containers/building-a-custom-container.md)
* [Community \(Public\) Notebooks](notebooks/public-notebooks.md)

## Projects

* [Overview](projects/about.md)
* [Managing Projects](projects/managing-projects.md)
* [GradientCI](projects/gradientci-v2/README.md)
  * [GradientCI V1 \(Deprecated\)](projects/gradientci-v2/gradientci-v2.md)
* [GitHub Badge - Run on Gradient](projects/github-badge-run-on-gradient.md)

## Experiments

* [Overview](experiments/about.md)
* [Using Experiments](experiments/using-experiments/README.md)
  * [Experiment options](experiments/using-experiments/experiment-options.md)
  * [Single-node & multi-node CLI options](experiments/using-experiments/single-node-and-multi-node-cli-options.md)
  * [Gradient Config File](experiments/using-experiments/gradient-config.yaml.md)
  * [Environment Variables](experiments/using-experiments/environment-variables.md)
  * [Experiment datasets](experiments/using-experiments/experiment-datasets.md)
  * [Git Commit Tracking](experiments/using-experiments/git-commit-tracking.md)
  * [Experiment Metrics](experiments/using-experiments/experiment-metrics/README.md)
    * [System Metrics](experiments/using-experiments/experiment-metrics/system-metrics.md)
    * [Custom Metrics](experiments/using-experiments/experiment-metrics/custom-metrics.md)
  * [Experiment Logs](experiments/using-experiments/experiment-logs.md)
  * [Experiment Ports](experiments/using-experiments/ports.md)
  * [GradientCI Experiments](experiments/using-experiments/gradientci-experiments.md)
  * [Diff Viewer](experiments/using-experiments/diff-viewer.md)
* [Distributed Training](experiments/distributed-training/README.md)
  * [Distributed Machine Learning with Tensorflow](experiments/distributed-training/multi-node-training.md)
  * [Distributed Machine Learning with MPI](experiments/distributed-training/distributed-machine-learning-with-mpi/README.md)
    * [Distributed Training using Horovod](experiments/distributed-training/distributed-machine-learning-with-mpi/distributed-training-using-horovod.md)
    * [Distributed Training Using ChainerMN](experiments/distributed-training/distributed-machine-learning-with-mpi/distributed-training-using-chainermn.md)
* [Hyperparameter Tuning](experiments/hyperparameters.md)
* [Containers](experiments/containers-public-and-private.md)

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
  * [Building Docker Containers with Jobs](jobs/create-a-job/building-docker-containers-with-jobs.md)
* [Public Jobs](jobs/public-jobs.md)

## Models

* [Overview](models/about.md)
* [Managing Models](models/create-a-model/README.md)
  * [Model Path, Parameters, & Metadata](models/create-a-model/model-path.md)
* [Example: Prepare a TensorFlow Model for Deployments](models/preparing-model-for-deployment.md)
* [Public Models](models/public-models.md)

## Deployments

* [Overview](deployments/about.md)
* [Managing Deployments](deployments/managing-deployments/README.md)
  * [Deployment States](deployments/managing-deployments/deployment-states.md)
  * [Deployment Logs](deployments/managing-deployments/deployment-logs.md)
  * [Deployment Metrics](deployments/managing-deployments/deployment-metrics.md)
  * [A Deployed Model's API Endpoint](deployments/managing-deployments/a-deployed-models-api-endpoint/README.md)
    * [Gradient + TensorFlow Serving](deployments/managing-deployments/a-deployed-models-api-endpoint/deployment-restful-api-tfserving.md)
  * [Deployment Autoscaling](deployments/managing-deployments/deployment-autoscaling.md)
  * [Optimize Models for Inference](deployments/managing-deployments/optimizing-tensorflow-models-for-inference.md)
* [Deployment Containers](deployments/deployment-containers/README.md)
  * [Custom Deployment Containers](deployments/deployment-containers/custom-deployment-containers.md)

## Data

* [Types of Storage](data/storage.md)
* [Storage Providers](data/storage-providers.md)
* [Datasets \(Preview\)](data/private-datasets-repository/README.md)
  * [\(Legacy\) S3 Datasets](data/private-datasets-repository/legacy-s3-datasets.md)
* [Managing Data in Gradient](data/managing-data-in-gradient/README.md)
  * [Managing Persistent Storage with VMs](data/managing-data-in-gradient/managing-persistent-storage-with-vms.md)
* [Public Datasets Repository](data/public-datasets-repository.md)

## TensorBoards

* [Overview](tensorboards/about.md)
* [Using Tensorboards in Gradient](tensorboards/using-tensorboards/README.md)
  * [TensorBoards getting started with Tensorflow](tensorboards/using-tensorboards/getting-started-with-tensorboards.md)

## Metrics

* [Metrics Overview](metrics/metrics-overview.md)
* [View and Query Metrics](metrics/quering-metrics.md)
* [Push Metrics](metrics/push-metrics.md)

## Secrets

* [Overview](secrets/overview.md)
* [Using Secrets](secrets/using-secrets.md)

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
  * [Destroy a Machine](machines/using-machines/destroy-machine.md)
  * [List Machines](machines/using-machines/list-machines.md)
  * [Show a Machine](machines/using-machines/show-machine.md)
  * [Wait For a Machine](machines/using-machines/wait-for-the-machine.md)
  * [Check a Machine's utilization](machines/using-machines/machine-utilization.md)
  * [Check availability](machines/using-machines/check-machine-availability.md)

## Instances

* [Instance Types](instances/instance-types.md)
* [Free Instances \(Free Tier\)](instances/free-instances.md)
* [Instance Tiers](instances/instance-tiers.md)
* [Preemptible Instances](instances/preemptible-instances.md)

## Tags

* [Overview](tags/overview.md)
* [Using Tags](tags/using-tags.md)

## Gradient Cluster <a id="gradient-private-cloud"></a>

* [Overview](gradient-private-cloud/about.md)
* [Setup](gradient-private-cloud/setup/README.md)
  * [Managed Private Clusters](gradient-private-cloud/setup/managed-installation.md)
  * [Self-Hosted Clusters](gradient-private-cloud/setup/self-hosted-clusters/README.md)
    * [Pre-installation steps](gradient-private-cloud/setup/self-hosted-clusters/pre-installation-steps.md)
    * [Gradient Installer CLI](gradient-private-cloud/setup/self-hosted-clusters/gradient-installer-cli.md)
    * [Terraform](gradient-private-cloud/setup/self-hosted-clusters/terraform/README.md)
      * [Pre-installation steps](gradient-private-cloud/setup/self-hosted-clusters/terraform/pre-installation-steps.md)
      * [Install on AWS](gradient-private-cloud/setup/self-hosted-clusters/terraform/install-on-aws.md)
      * [Install on bare metal / VMs](gradient-private-cloud/setup/self-hosted-clusters/terraform/bare-metal-vms.md)
      * [Install on NVIDIA DGX](gradient-private-cloud/setup/self-hosted-clusters/terraform/install-nvidia-dgx.md)
    * [Let's Encrypt DNS Providers](gradient-private-cloud/setup/self-hosted-clusters/lets-encrypt-dns-providers.md)
    * [Updating your cluster](gradient-private-cloud/setup/self-hosted-clusters/updating-your-cluster.md)
* [Usage](gradient-private-cloud/usage.md)

## Paperspace Account

* [Creating a Team](paperspace-account/creating-a-team.md)
* [Overview](paperspace-account/overview.md)
* [Public Profiles](paperspace-account/gradient-public-profiles.md)
* [Hotkeys](paperspace-account/hotkeys.md)

## Release Notes

* [Product release notes](https://updates.paperspace.com/)
* [CLI/SDK Release notes](https://github.com/Paperspace/gradient-cli/releases)

