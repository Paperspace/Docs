# Quick Start

## Prerequisites

To begin using Gradient, follow these preliminary steps:

1. [Create a Paperspace account ](https://console.paperspace.com/signup?gradient=true)
2. Optional: [Create a team ](https://support.paperspace.com/hc/en-us/articles/360010359213-Creating-and-Managing-Paperspace-Teams)to invite collaborators

Now you can create Notebooks, Workflows, Models, Deployments, and more!  Note: if you are self-hosting Gradient, please visit the [Gradient Private Cloud ](../../gradient-private-cloud/about/setup/self-hosted-clusters/)section for more info.

## Logging into the Paperspace Console for the first time

When you first log into the Paperspace Console, you must first select the Gradient from the product dropdown:

![](../../.gitbook/assets/image%20%2832%29.png)

## Create a Notebook

Notebooks can be created on the Notebooks tab. Just select a [template](../../explore-train-deploy/about/create-a-notebook/notebook-containers/), choose your [instance type](../../more/instance-types/), and then click create. 

{% hint style="success" %}
Check out the [FREE GPU](../../more/instance-types/free-instances.md) option when launching Notebooks!
{% endhint %}

![Select Notebooks &amp;gt; Create a Notebook to enter the notebook create flow](../../.gitbook/assets/screen-shot-2021-04-18-at-10.00.21-pm.png)

{% hint style="success" %}
Check out the [ML Showcase](https://ml-showcase.paperspace.com/) for a list of projects you can fork into your own account
{% endhint %}

You can stop, start, fork, and swap out the instance type anytime. Choose from a wide selection of pre-configured templates or bring your own. View the overview video to learn more:

{% embed url="https://www.youtube.com/watch?v=i4pvLzvw2ME" caption="Learn how to create a Jupyter Notebook. 1m48s." %}

## Advanced MLOps

{% hint style="warning" %}
Using advanced ML components contained within Projects requires [creating a cluster](../../gradient-private-cloud/about/setup/managed-installation.md).   
{% endhint %}

### Create a Project

Projects organize your work.  To create a Project, navigate to **Gradient** &gt; **Projects** in the UI and click **Create Project**, provide a name, and click **create**. 

![](../../.gitbook/assets/image%20%2826%29.png)

### Running your first Workflow

You can run Workflows from the web interface or CLI:

{% hint style="info" %}
Before creating an experiment using the CLI, you must first [install the CLI](install-the-cli.md). 
{% endhint %}

**Run a sample Workflow**

The following command will work and will create and start an Experiment that will display properties of the attached GPU. Be sure to replace `<your-project-id>` with your **Project ID** and `<your-cluster-id>` with your **Cluster ID**.

{% hint style="info" %}
**Note:** We recommend stashing your API key with `gradient apiKey XXXXXXXXXXXXX` or you can add your API key as an option on each Experiment. See [Connecting Your Account](install-the-cli.md#connecting-your-account).
{% endhint %}

```bash
gradient workflows run --projectId <your-project-id> --clusterId <your-cluster-id> --container 'Test-Container' --machineType P4000 --command 'nvidia-smi' --name 'test-01' --workspace none --apiKey <your-api-key>
```

![](../../.gitbook/assets/screen-shot-2020-10-09-at-6.40.00-pm.png)

Behind the scenes, your Workflow will be executed on your cluster starting with the command you provided. You can always use the `--help` option after any command in the CLI for more info.  

Congratulations! You ran your first Experiment on Gradient 🚀

## Explore the rest of the platform

From [Models](../../data/models/) to [Deployments](../../explore-train-deploy/deployments-overview/), there's a lot more to the Gradient platform.  We recommend using the Web UI to explore the primary components and also be sure to install the [CLI](install-the-cli.md) and check out the [SDK](../../more/gradient-python-sdk-1/).

