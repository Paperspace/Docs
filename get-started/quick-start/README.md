# Quick Start

## Prerequisites

To begin using Gradient, follow these preliminary steps:

1. [Create a Paperspace account ](https://console.paperspace.com/signup?gradient=true)
2. Optional: [Create a team ](https://support.paperspace.com/hc/en-us/articles/360010359213-Creating-and-Managing-Paperspace-Teams)to invite collaborators

Now you can create Notebooks, Workflows, Models, Deployments, and more!  Note: if you are self-hosting Gradient, please visit the [Gradient Private Cloud ](../../gradient-private-cloud/about/setup/self-hosted-clusters/)section for more info.

{% hint style="info" %}
In order to unlock Deployments, please [contact](https://info.paperspace.com/contact-sales-gradient) our solutions team. 
{% endhint %}

## Logging in for the first time

When you first log into the Paperspace Console, you can select Gradient from the product dropdown:

![](../../.gitbook/assets/image%20%2832%29.png)

## Create a Notebook

Notebooks can be created on the Notebooks tab. Just select a [template](../../explore-train-deploy/notebooks/create-a-notebook/notebook-containers/), choose your [instance type](../../more/instance-types/), and then click create. 

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

You can perform advanced MLOps functions using Workflows, Models and Deployments. Workflows allow you to work with Data, Models, and Deployment in a reproducible and fully tracked manner.  You can define a workflow one time using a text editor and use it repeatedly to perform simple or complext ML activities, such as pre-processing data, training a model, creating a deployment, or performing inference.

{% hint style="warning" %}
In order to unlock Deployments, please [contact](https://info.paperspace.com/contact-sales-gradient) our solutions team. 
{% endhint %}

### Create a Project

Projects organize your work.  To create a Project, navigate to **Projects** and click **Create Project**, provide a name, and click **create**. 

![](../../.gitbook/assets/screen-shot-2021-04-22-at-11.46.07-am.png)

Make a note of the projectId, for example `pr1234567`.

### Running your first Workflow

You can run Workflows from the web interface or CLI. First you need to create a new Workflow. This will allow you to keep track of related runs of the Workflow.

If you have never run a workflow before you can create and run a demo workflow all in one step in the web interface, by clicking on the Workflows tab within the project, then clicking the **Create Your First Workflow** button.

![](../../.gitbook/assets/screen-shot-2021-04-22-at-12.06.01-pm.png)

From here you can either run the workflow as-is, or download the Workflow spec to your workstations and run it from the CLI.

### **Steps to create and run a Workflow from the CLI**

1. \*\*\*\*[**Install the Gradient CLI**](install-the-cli.md)\*\*\*\*
2. \*\*\*\*[**Connect your account**](install-the-cli.md#connecting-your-account)\*\*\*\*
3. **Create a  Workflow**

Specify a name for the Workflow and a projectId.  You can use the projectId from project created earlier.

```bash
gradient workflows create  \ 
--name <your-workflow-name>  \
--projectId <your-project-id>
```

4. **Download or copy the sample Workflow YAML file from the web interface to your computer**

Place the contents in a file named `workflow.yaml`.

5. **Run the Workflow from the CLI**

The following command will run an instance of the Workflow in your project. Be sure to replace `<your-workflow-id>` with your **Workflow ID**.

```bash
gradient workflows run  \ 
--id <your-workflow-id>  \
--path ./workflow.yaml 
```

{% hint style="info" %}
**Note:** We recommend stashing your API key with `gradient apiKey XXXXXXXXXXXXX` or you can add your API key as an option on each command. See [Connecting Your Account](install-the-cli.md#connecting-your-account).
{% endhint %}


Behind the scenes, your Workflow will be executed on the Gradient public cluster. Congratulations! You ran your first Workflow on Gradient 🚀

## Explore the rest of the platform

From [Models](../../data/models/) to [Deployments](../../explore-train-deploy/deployments/), there's a lot more to the Gradient platform.  We recommend using the Web UI to explore the primary components and also be sure to install the [CLI](install-the-cli.md) and check out the [SDK](../../more/gradient-python-sdk-1/).

