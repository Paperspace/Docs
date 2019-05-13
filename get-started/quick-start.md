# Quick Start

## Prerequisites 

1. [Create a Paperspace account ](https://www.paperspace.com/account/signup)
2. [Install the Paperspace Command Line Interface ](install-the-cli.md#installation)
3. [Connecting your account](install-the-cli.md#connecting-your-account)

## Create a Notebook

Notebooks can be created by clicking _Create Notebook_ button on the Notebooks tab. You can stop, start, fork, and swap out the instance type anytime. Choose from a wide selection of pre-configured templates or bring your own.  See more info [here](../notebooks/about.md).

![](../.gitbook/assets/image%20%2818%29.png)

## Submit an Experiment

You can run Experiments from the web interface or CLI:

### Experiment Builder interface

![](../.gitbook/assets/image%20%283%29.png)

### CLI

```bash
paperspace-python experiments createAndStart singlenode --projectHandle prj0ztwij --container Test-Container --machineType P4000 --command "nvidia-smi --name test-01
```

Your Experiment will get uploaded to our cluster of machines. Behind the scenes, we are creating a Docker container, and running the command you provided. There are several optional Experiment parameters.  

### Monitor your Experiment progress

Experiments states go from **Queued** &gt; **Pending** &gt; **Running**  Once the Experiment is in a **Running** state, you can watch your Job run in the CLI and web UI.  An Experiment can complete with the following states: **Success**, **Cancelled**, or **Error**.

 Congratulations! You ran your first job on Gradient 🚀

Jobs have a ton of functionality that this quick example doesn't cover.  To learn more, view the [Experiments section](../experiments/about.md).

