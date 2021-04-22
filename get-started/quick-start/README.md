# Quick Start

## Prerequisites

To begin using Gradient, follow these preliminary steps:

1. [Create a Paperspace account ](https://console.paperspace.com/signup?gradient=true)
2. Optional: [Create a team ](https://support.paperspace.com/hc/en-us/articles/360010359213-Creating-and-Managing-Paperspace-Teams)to invite collaborators

Now you can create Notebooks, Workflows, Models, Deployments, and more!  Note: if you are self-hosting Gradient, please visit the [Gradient Private Cloud ](../../gradient-private-cloud/about/setup/self-hosted-clusters/)section for more info.

{% hint style="info" %}
In order to unlock Workflows, Models, and Deployments, please [contact](https://info.paperspace.com/contact-sales-gradient) our solutions team. 
{% endhint %}

## Logging in for the first time

When you first log into the Paperspace Console, you can select Gradient from the product dropdown:

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
In order to unlock Workflows, Models, and Deployments, please [contact](https://info.paperspace.com/contact-sales-gradient) our solutions team. 
{% endhint %}

### Create a Project

Projects organize your work.  To create a Project, navigate to **Gradient** &gt; **Projects** in the UI and click **Create Project**, provide a name, and click **create**. 

![](../../.gitbook/assets/screen-shot-2021-04-22-at-11.46.07-am.png)

### Running your first Workflow

{% hint style="warning" %}
Using Workflows requires [creating a cluster](../../gradient-private-cloud/about/setup/managed-installation.md).  
{% endhint %}

You can run Workflows from the web interface or CLI. The first step is to create a new Workflow.

![](../../.gitbook/assets/screen-shot-2021-04-22-at-12.06.01-pm.png)

### **Steps**

1. \*\*\*\*[**Install the CLI**](install-the-cli.md)\*\*\*\*
2. **Download or copy the sample Workflow YAML file to your computer**
3. **Run the Workflow from the CLI**

```bash
gradient workflows run  \ 
--id <your-workflow-id>  \
--clusterId <your-cluster-id>  \
--path ./workflow.yaml 
```

{% hint style="info" %}
**Note:** We recommend stashing your API key with `gradient apiKey XXXXXXXXXXXXX` or you can add your API key as an option on each Experiment. See [Connecting Your Account](install-the-cli.md#connecting-your-account).
{% endhint %}

The following command will create and start a Workflow that will run a sample project. Be sure to replace `<your-workflow-id>` with your **Workflow ID** and `<your-cluster-id>` with your **Cluster ID**.

Behind the scenes, your Workflow will be executed on your cluster. Congratulations! You ran your first Workflow on Gradient 🚀

## Explore the rest of the platform

From [Models](../../data/models/) to [Deployments](../../explore-train-deploy/deployments-overview/), there's a lot more to the Gradient platform.  We recommend using the Web UI to explore the primary components and also be sure to install the [CLI](install-the-cli.md) and check out the [SDK](../../more/gradient-python-sdk-1/).

