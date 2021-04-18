# Table of contents

* [About Paperspace Gradient](README.md)

## Get Started

* [Quick Start](get-started/quick-start.md)
* [Core Concepts](get-started/core-concepts.md)
* [Install the Gradient CLI](get-started/install-the-cli.md)
* [Common Errors](get-started/error-codes.md)

## Tutorials

* [Tutorials List](tutorials/tutorials-list/README.md)
  * [Getting Started with Notebooks](tutorials/tutorials-list/getting-started-with-gradient-notebooks.md)
  * [Train a Model with the Web UI](tutorials/tutorials-list/train-a-model-with-the-ui.md)
  * [Train a Model with the CLI](tutorials/tutorials-list/train-a-model-with-the-cli.md)
  * [Advanced: Distributed training sample project](tutorials/tutorials-list/advanced-distributed-training-sample-project.md)
  * [Registering Models in Gradient](tutorials/tutorials-list/registering-models-in-gradient.md)
  * [Using Gradient Deployments](tutorials/tutorials-list/dealing-with-gradient-deployments.md)
  * [Using Custom Containers](tutorials/tutorials-list/using-custom-containers-with-gradient.md)

## Notebooks

* [Overview](notebooks/about.md)
* [Using Notebooks](notebooks/create-a-notebook/README.md)
  * [The Notebook interface](notebooks/create-a-notebook/the-notebook-interface.md)
  * [Notebook metrics](notebooks/create-a-notebook/notebook-metrics.md)
  * [Share a Notebook](notebooks/create-a-notebook/share-a-notebook.md)
  * [Fork a Notebook](notebooks/create-a-notebook/fork-a-notebook.md)
  * [Notebook Directories](notebooks/create-a-notebook/notebooks-directories.md)
  * [Notebook Containers](notebooks/create-a-notebook/notebook-containers/README.md)
    * [Building a Custom Container](notebooks/create-a-notebook/notebook-containers/building-a-custom-container.md)
  * [Notebook Workspace Include Files](notebooks/create-a-notebook/notebook-include.md)
  * [Community \(Public\) Notebooks](notebooks/create-a-notebook/public-notebooks.md)
* [ML Showcase](notebooks/ml-showcase.md)
* [Run on Gradient \(GitHub badge\)](notebooks/github-badge-run-on-gradient.md)

## Projects

* [Overview](projects/about.md)
* [Managing Projects](projects/managing-projects.md)
* [GradientCI](projects/gradientci-v2/README.md)
  * [GradientCI V1 \(Deprecated\)](projects/gradientci-v2/gradientci-v2.md)

## Workflows

* [Overview](workflows/overview/README.md)
  * [Getting Started with Workflows](workflows/overview/getting-started-with-workflows.md)
  * [Workflow Spec](workflows/overview/workflow-spec.md)
  * [Gradient Actions](workflows/overview/gradient-actions.md)

## Models

* [Overview](models/about.md)
* [Managing Models](models/create-a-model/README.md)
  * [Example: Prepare a TensorFlow Model for Deployments](models/create-a-model/preparing-model-for-deployment.md)
  * [Model Path, Parameters, & Metadata](models/create-a-model/model-path.md)
* [Public Models](models/public-models.md)

## Deployments

* [Overview](deployments/about.md)
* [Managing Deployments](deployments/managing-deployments/README.md)
  * [Deployment Containers](deployments/managing-deployments/deployment-containers/README.md)
    * [Custom Deployment Containers](deployments/managing-deployments/deployment-containers/custom-deployment-containers.md)
  * [Deployment States](deployments/managing-deployments/deployment-states.md)
  * [Deployment Logs](deployments/managing-deployments/deployment-logs.md)
  * [Deployment Metrics](deployments/managing-deployments/deployment-metrics.md)
  * [A Deployed Model's API Endpoint](deployments/managing-deployments/a-deployed-models-api-endpoint/README.md)
    * [Gradient + TensorFlow Serving](deployments/managing-deployments/a-deployed-models-api-endpoint/deployment-restful-api-tfserving.md)
  * [Deployment Autoscaling](deployments/managing-deployments/deployment-autoscaling.md)
  * [Optimize Models for Inference](deployments/managing-deployments/optimizing-tensorflow-models-for-inference.md)

## Data

* [Types of Storage](data/storage/README.md)
  * [Managing Data in Gradient](data/storage/managing-data-in-gradient/README.md)
    * [Managing Persistent Storage with VMs](data/storage/managing-data-in-gradient/managing-persistent-storage-with-vms.md)
* [Storage Providers](data/storage-providers.md)
* [Versioned Datasets](data/private-datasets-repository.md)
* [Public Datasets Repository](data/public-datasets-repository.md)

## Metrics

* [Metrics Overview](metrics/metrics-overview.md)
* [View and Query Metrics](metrics/quering-metrics.md)
* [Push Metrics](metrics/push-metrics.md)

## Secrets

* [Overview](secrets/overview.md)
* [Using Secrets](secrets/using-secrets.md)

## Gradient SDK <a id="gradient-python-sdk"></a>

* [Gradient SDK Overview](gradient-python-sdk/gradient-python-sdk/README.md)
  * [Projects Client](gradient-python-sdk/gradient-python-sdk/projects-client.md)
  * [Experiments Client](gradient-python-sdk/gradient-python-sdk/experiments-client.md)
  * [Models Client](gradient-python-sdk/gradient-python-sdk/models-client.md)
  * [Deployments Client](gradient-python-sdk/gradient-python-sdk/deployments-client.md)
  * [Jobs Client](gradient-python-sdk/gradient-python-sdk/jobs-client.md)
* [End to end tutorial](gradient-python-sdk/sdk-tutorial.md)
* [Full SDK Reference](https://paperspace.github.io/gradient-cli/gradient.api_sdk.clients.html)

## Instances

* [Instance Types](instances/instance-types/README.md)
  * [Free Instances \(Free Tier\)](instances/instance-types/free-instances.md)
  * [Instance Tiers](instances/instance-types/instance-tiers.md)

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

## Tags

* [Overview](tags/overview.md)
* [Using Tags](tags/using-tags.md)

## Paperspace Account

* [Overview](paperspace-account/overview.md)
* [Public Profiles](paperspace-account/gradient-public-profiles.md)
* [Billing & Subscriptions](paperspace-account/billing-and-subscriptions.md)
* [Hotkeys](paperspace-account/hotkeys.md)
* [Teams](paperspace-account/teams/README.md)
  * [Creating a Team](paperspace-account/teams/creating-a-team.md)
  * [Upgrading to a Team Plan](paperspace-account/teams/upgrading-to-a-team-plan.md)

## Release Notes

* [Product release notes](https://updates.paperspace.com/)
* [CLI/SDK Release notes](https://github.com/Paperspace/gradient-cli/releases)

