# Quick Start

## Prerequisites

To begin using Gradient, follow these preliminary steps:

1. [Create a Paperspace account ](https://www.paperspace.com/account/signup)
2. Create a team if higher tiers of service and collaboration features are desired
3. [Install the Gradient CLI ](install-the-cli.md#installation)
4. [Connecting your account](install-the-cli.md#connecting-your-account)

Now you can create Notebooks, Jobs, Projects, Experiments, Deployments, and more!

## Create a Notebook

Notebooks can be created by clicking _Create Notebook_ button on the Notebooks tab. You can stop, start, fork, and swap out the instance type anytime. Choose from a wide selection of pre-configured templates or bring your own. See more info [here](../notebooks/about.md).

![](../.gitbook/assets/image%20%2824%29.png)

## Submit an Experiment

You can run Experiments from the web interface or CLI:

### Using the Experiment Builder \(UI\)

![](../.gitbook/assets/image%20%285%29.png)

### Using the CLI

Before creating an experiment using the CLI, you must first create a Project for your Experiments to live in. To create a Project, navigate to **Gradient** &gt; **Projects** in the UI and click **Create Project**. Then select **Create Standalone Project** and provide a project name. Now, you can use the created Project's **Project ID** in order to create Experiments in that Project via the CLI.

**Example command**

The following command will work and will create and start an Experiment that will display properties of the attached GPU. Be sure to replace `<your-project-id>` with your **Project ID**.

{% hint style="info" %}
**Note:** We recommend stashing your API key with `gradient apiKey XXXXXXXXXXXXX` or you can add your API key as an option on each Experiment. See [Connecting Your Account](install-the-cli.md#connecting-your-account).
{% endhint %}

```bash
gradient experiments run singlenode --projectId <your-project-id> --container 'Test-Container' --machineType P4000 --command 'nvidia-smi' --name 'test-01' --workspaceUrl none --apiKey <your-api-key>
```

You can also create `multi-node` and `hyperparameter` Experiments, and you can use the `create` command to simply create Experiments that can be started later. Explore all the advanced options [here](../experiments/run-experiments-cli.md).

Behind the scenes, your Experiment will be uploaded and executed on our cluster of machines starting with the command you provided. There are [several optional Experiment parameters](https://docs.paperspace.com/gradient/experiments/run-experiments#parameters-common-to-both-experiment-types), such as to specify your **workspace** \(the additional files to be used in your experiment\). You can always use the `--help` option after any command in the CLI for more info.

### Monitor your Experiment progress

Experiments states transition from **Queued** &gt; **Pending** &gt; **Running**. Once the Experiment is in the **Running** state, you can watch your Experiment run in the CLI and web UI. An Experiment can complete with the following states: **Success, Cancelled, Error,** or **Failed**.

Congratulations! You ran your first Experiment on Gradient 🚀

Experiments have a ton of functionality that this quick example doesn't cover. To learn more, view the [Experiments section](../experiments/about.md).

