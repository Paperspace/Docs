# Table of contents

* [About Paperspace Gradient](README.md)

## Get Started

* [Quick Start](get-started/quick-start.md)
* [Core Concepts](get-started/core-concepts/README.md)
  * [Install the Gradient CLI](get-started/core-concepts/install-the-cli.md)
  * [Common Errors](get-started/core-concepts/error-codes.md)
* [Organizing Projects](get-started/managing-projects/README.md)
  * [Secrets](get-started/managing-projects/using-secrets.md)
* [Tutorials](get-started/tutorials-list/README.md)
  * [Get started with Notebooks](get-started/tutorials-list/getting-started-with-gradient-notebooks.md)
  * [End-to-end example](get-started/tutorials-list/end-to-end-example.md)
  * [Workflows sample project](get-started/tutorials-list/workflows-sample-project.md)
  * [Managing Models](get-started/tutorials-list/registering-models-in-gradient.md)
  * [Using Deployments](get-started/tutorials-list/dealing-with-gradient-deployments.md)

## Primary Components <a id="using-gradient"></a>

* [Notebooks](using-gradient/about/README.md)
  * [Run on Gradient \(GitHub badge\)](using-gradient/about/github-badge-run-on-gradient.md)
  * [ML Showcase](using-gradient/about/ml-showcase.md)
  * [Using Notebooks](using-gradient/about/create-a-notebook/README.md)
    * [The Notebook interface](using-gradient/about/create-a-notebook/the-notebook-interface.md)
    * [Notebook metrics](using-gradient/about/create-a-notebook/notebook-metrics.md)
    * [Share a Notebook](using-gradient/about/create-a-notebook/share-a-notebook.md)
    * [Fork a Notebook](using-gradient/about/create-a-notebook/fork-a-notebook.md)
    * [Notebook Directories](using-gradient/about/create-a-notebook/notebooks-directories.md)
    * [Notebook Containers](using-gradient/about/create-a-notebook/notebook-containers/README.md)
      * [Building a Custom Container](using-gradient/about/create-a-notebook/notebook-containers/building-a-custom-container.md)
    * [Notebook Workspace Include Files](using-gradient/about/create-a-notebook/notebook-include.md)
    * [Community \(Public\) Notebooks](using-gradient/about/create-a-notebook/public-notebooks.md)
* [Workflows](using-gradient/workflows-1/README.md)
  * [Getting Started with Workflows](using-gradient/workflows-1/getting-started-with-workflows.md)
  * [Workflow Spec](using-gradient/workflows-1/workflow-spec.md)
  * [Gradient Actions](using-gradient/workflows-1/gradient-actions.md)
* [Deployments](using-gradient/deployments-overview/README.md)
  * [Managing Deployments](using-gradient/deployments-overview/managing-deployments/README.md)
    * [Deployment Containers](using-gradient/deployments-overview/managing-deployments/deployment-containers/README.md)
      * [Custom Deployment Containers](using-gradient/deployments-overview/managing-deployments/deployment-containers/custom-deployment-containers.md)
    * [Deployment States](using-gradient/deployments-overview/managing-deployments/deployment-states.md)
    * [Deployment Logs](using-gradient/deployments-overview/managing-deployments/deployment-logs.md)
    * [Deployment Metrics](using-gradient/deployments-overview/managing-deployments/deployment-metrics.md)
    * [A Deployed Model's API Endpoint](using-gradient/deployments-overview/managing-deployments/a-deployed-models-api-endpoint/README.md)
      * [Gradient + TensorFlow Serving](using-gradient/deployments-overview/managing-deployments/a-deployed-models-api-endpoint/deployment-restful-api-tfserving.md)
    * [Deployment Autoscaling](using-gradient/deployments-overview/managing-deployments/deployment-autoscaling.md)
    * [Optimize Models for Inference](using-gradient/deployments-overview/managing-deployments/optimizing-tensorflow-models-for-inference.md)

## Secondary Components <a id="data"></a>

* [Data](data/data-overview/README.md)
  * [Versioned Datasets](data/data-overview/private-datasets-repository/README.md)
    * [Public Datasets Repository](data/data-overview/private-datasets-repository/public-datasets-repository.md)
    * [Storage Providers](data/data-overview/private-datasets-repository/storage-providers.md)
  * [Persistent Storage](data/data-overview/persistent-storage.md)
* [Models](data/models/README.md)
  * [Managing Models](data/models/create-a-model/README.md)
    * [Public Models](data/models/create-a-model/public-models.md)
    * [Example: Prepare a TensorFlow Model for Deployments](data/models/create-a-model/preparing-model-for-deployment.md)
    * [Model Path, Parameters, & Metadata](data/models/create-a-model/model-path.md)

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

---

* [Metrics Overview](metrics-overview/README.md)
  * [Push Metrics](metrics-overview/push-metrics.md)
  * [View & Query Metrics](metrics-overview/quering-metrics.md)
* [Instance Types](instance-types/README.md)
  * [Free Instances \(Free Tier\)](instance-types/free-instances.md)
  * [Instance Tiers](instance-types/instance-tiers.md)
* [SDK Overview](gradient-python-sdk-1/README.md)
  * [End to end tutorial](gradient-python-sdk-1/sdk-tutorial.md)
  * [Projects Client](gradient-python-sdk-1/projects-client.md)
  * [Models Client](gradient-python-sdk-1/models-client.md)
  * [Deployments Client](gradient-python-sdk-1/deployments-client.md)
  * [Full SDK Reference](https://paperspace.github.io/gradient-cli/gradient.api_sdk.clients.html)

## Paperspace Account

* [Your Account](paperspace-account/overview/README.md)
  * [Teams](paperspace-account/overview/teams/README.md)
    * [Creating a Team](paperspace-account/overview/teams/creating-a-team.md)
    * [Upgrading to a Team Plan](paperspace-account/overview/teams/upgrading-to-a-team-plan.md)
  * [Hotkeys](paperspace-account/overview/hotkeys.md)
  * [Billing & Subscriptions](paperspace-account/overview/billing-and-subscriptions.md)
  * [Public Profiles](paperspace-account/overview/gradient-public-profiles.md)

---

* [Release notes](https://updates.paperspace.com/)

## More

* [Untitled](more/untitled.md)

