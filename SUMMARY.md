# Table of contents

* [About Paperspace Gradient](README.md)

## Get Started

* [Quick Start](get-started/quick-start.md)
* [Core Concepts](get-started/core-concepts/README.md)
  * [Install the Gradient CLI](get-started/core-concepts/install-the-cli.md)
  * [Common Errors](get-started/core-concepts/error-codes.md)
* [Projects](get-started/about-projects/README.md)
  * [Managing Projects](get-started/about-projects/managing-projects.md)
* [Tutorials](get-started/tutorials-list/README.md)
  * [Get started with Notebooks](get-started/tutorials-list/getting-started-with-gradient-notebooks.md)
  * [End-to-end example](get-started/tutorials-list/end-to-end-example.md)
  * [Workflows sample project](get-started/tutorials-list/workflows-sample-project.md)
  * [Managing Models](get-started/tutorials-list/registering-models-in-gradient.md)
  * [Using Deployments](get-started/tutorials-list/dealing-with-gradient-deployments.md)

## Notebooks

* [Overview](notebooks/about/README.md)
  * [Using Notebooks](notebooks/about/create-a-notebook/README.md)
    * [The Notebook interface](notebooks/about/create-a-notebook/the-notebook-interface.md)
    * [Notebook metrics](notebooks/about/create-a-notebook/notebook-metrics.md)
    * [Share a Notebook](notebooks/about/create-a-notebook/share-a-notebook.md)
    * [Fork a Notebook](notebooks/about/create-a-notebook/fork-a-notebook.md)
    * [Notebook Directories](notebooks/about/create-a-notebook/notebooks-directories.md)
    * [Notebook Containers](notebooks/about/create-a-notebook/notebook-containers/README.md)
      * [Building a Custom Container](notebooks/about/create-a-notebook/notebook-containers/building-a-custom-container.md)
    * [Notebook Workspace Include Files](notebooks/about/create-a-notebook/notebook-include.md)
    * [Community \(Public\) Notebooks](notebooks/about/create-a-notebook/public-notebooks.md)
* [ML Showcase](notebooks/ml-showcase.md)
* [Run on Gradient \(GitHub badge\)](notebooks/github-badge-run-on-gradient.md)

## Workflows

* [Overview](workflows/overview/README.md)
  * [Getting Started with Workflows](workflows/overview/getting-started-with-workflows.md)
  * [Workflow Spec](workflows/overview/workflow-spec.md)
  * [Gradient Actions](workflows/overview/gradient-actions.md)

## Models

* [Overview](models/about/README.md)
  * [Managing Models](models/about/create-a-model/README.md)
    * [Public Models](models/about/create-a-model/public-models.md)
    * [Example: Prepare a TensorFlow Model for Deployments](models/about/create-a-model/preparing-model-for-deployment.md)
    * [Model Path, Parameters, & Metadata](models/about/create-a-model/model-path.md)

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

* [Data Overview](data/storage/README.md)
  * [Managing Persistent Storage](data/storage/managing-data-in-gradient.md)
* [Versioned Datasets](data/private-datasets-repository/README.md)
  * [Public Datasets Repository](data/private-datasets-repository/public-datasets-repository.md)
  * [Storage Providers](data/private-datasets-repository/storage-providers.md)

---

* [Metrics Overview](metrics-overview/README.md)
  * [Push Metrics](metrics-overview/push-metrics.md)
  * [View & Query Metrics](metrics-overview/quering-metrics.md)
* [Secrets Overview](overview/README.md)
  * [Using Secrets](overview/using-secrets.md)
* [Instance Types](instance-types/README.md)
  * [Free Instances \(Free Tier\)](instance-types/free-instances.md)
  * [Instance Tiers](instance-types/instance-tiers.md)

## Gradient SDK <a id="gradient-python-sdk"></a>

* [SDK Overview](gradient-python-sdk/gradient-python-sdk/README.md)
  * [End to end tutorial](gradient-python-sdk/gradient-python-sdk/sdk-tutorial.md)
  * [Projects Client](gradient-python-sdk/gradient-python-sdk/projects-client.md)
  * [Models Client](gradient-python-sdk/gradient-python-sdk/models-client.md)
  * [Deployments Client](gradient-python-sdk/gradient-python-sdk/deployments-client.md)
  * [Full SDK Reference](https://paperspace.github.io/gradient-cli/gradient.api_sdk.clients.html)

## Gradient Cluster <a id="gradient-private-cloud"></a>

* [Overview](gradient-private-cloud/about/README.md)
  * [Setup](gradient-private-cloud/about/setup/README.md)
    * [Managed Private Clusters](gradient-private-cloud/about/setup/managed-installation.md)
    * [Self-Hosted Clusters](gradient-private-cloud/about/setup/self-hosted-clusters/README.md)
      * [Pre-installation steps](gradient-private-cloud/about/setup/self-hosted-clusters/pre-installation-steps.md)
      * [Gradient Installer CLI](gradient-private-cloud/about/setup/self-hosted-clusters/gradient-installer-cli.md)
      * [Terraform](gradient-private-cloud/about/setup/self-hosted-clusters/terraform/README.md)
        * [Pre-installation steps](gradient-private-cloud/about/setup/self-hosted-clusters/terraform/pre-installation-steps.md)
        * [Install on AWS](gradient-private-cloud/about/setup/self-hosted-clusters/terraform/install-on-aws.md)
        * [Install on bare metal / VMs](gradient-private-cloud/about/setup/self-hosted-clusters/terraform/bare-metal-vms.md)
        * [Install on NVIDIA DGX](gradient-private-cloud/about/setup/self-hosted-clusters/terraform/install-nvidia-dgx.md)
      * [Let's Encrypt DNS Providers](gradient-private-cloud/about/setup/self-hosted-clusters/lets-encrypt-dns-providers.md)
      * [Updating your cluster](gradient-private-cloud/about/setup/self-hosted-clusters/updating-your-cluster.md)
  * [Usage](gradient-private-cloud/about/usage.md)

## Paperspace Account

* [Your Account](paperspace-account/overview/README.md)
  * [Teams](paperspace-account/overview/teams/README.md)
    * [Creating a Team](paperspace-account/overview/teams/creating-a-team.md)
    * [Upgrading to a Team Plan](paperspace-account/overview/teams/upgrading-to-a-team-plan.md)
  * [Hotkeys](paperspace-account/overview/hotkeys.md)
  * [Billing & Subscriptions](paperspace-account/overview/billing-and-subscriptions.md)
  * [Public Profiles](paperspace-account/overview/gradient-public-profiles.md)

## Release Notes

* [Product release notes](https://updates.paperspace.com/)
* [CLI/SDK Release notes](https://github.com/Paperspace/gradient-cli/releases)

