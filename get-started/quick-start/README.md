# Quick Start

## Prerequisites

To begin using Gradient, follow these preliminary steps:

1. [Create a Paperspace account ](https://console.paperspace.com/signup?gradient=true)
2. Optional: [Create a team ](https://support.paperspace.com/hc/en-us/articles/360010359213-Creating-and-Managing-Paperspace-Teams)to invite collaborators

Now you can create Notebooks, Workflows, Deployments, and more!&#x20;

{% embed url="https://youtu.be/XW1RyPZ_b0g" %}

## Logging in for the first time

When you first log into the Paperspace Console, you can select Gradient from the product dropdown:

![](<../../.gitbook/assets/image (32).png>)

## First Create a Project

Projects help organize your work. To get started, just choose a name and click create.

![](../../.gitbook/assets/project\_create\_2.png)

## Create a Notebook

After creating a Project, Notebooks can be created on the Notebooks tab within the Project. Just select a [template](../../explore-train-deploy/notebooks/create-a-notebook/notebook-containers/), choose your [instance type](../../more/instance-types/), and then click create.

{% hint style="success" %}
Check out the [FREE GPU](../../more/instance-types/free-instances.md) option when launching Notebooks!
{% endhint %}

![](../../.gitbook/assets/notebook\_create.png)

{% hint style="success" %}
Check out the [ML Showcase](https://ml-showcase.paperspace.com) for a list of projects you can fork into your own account
{% endhint %}

You can stop, start, fork, and swap out the instance type anytime. Choose from a wide selection of pre-configured templates or bring your own.&#x20;

## Create a Workflow

You can automate machine learning tasks using Workflows. You can define a workflow once and use it repeatedly to perform simple or complex MLOps activities, such as pre-processing data, training models, and creating or updating deployments.

![](../../.gitbook/assets/workflow\_create.png)

### Run a Workflow from a GitHub trigger (recommended)

This requires the project to be linked to a GitHub repository. Follow the instructions on the page to install the Gradient **Github App** into your Github account, and select the git repo you want to associate with project. Alternatively you can select one of the **sample repos.** &#x20;

If you choose to use your own git repo, you will be prompted to add a YAML file to your repo that defines the Workflow steps.&#x20;

### **Run a Workflow from the CLI (advanced)**

1. [**Install the Gradient CLI**](install-the-cli.md)
2. [**Connect your account**](install-the-cli.md#connecting-your-account)
3.  **Create a Workflow**

    This step is only needed if you didn't already create a default `demo workflow` in the web interface. Specify a name for the Workflow and a `projectId`. Use the `projectId` from the project you created earlier.

    ```bash
    gradient workflows create  \ 
    --name <your-workflow-name>  \
    --projectId <your-project-id>
    ```

    To see a list of your projects and `projectIds` run `gradient projects list`. For a list of Workflows within a project run `gradient workflows list --projectId <your-project-id>`.
4.  **Download or copy the sample Workflow Spec to your computer**

    Here is the Workflow Spec for reference:

    ```yaml
    jobs:
      CloneRepo:
        resources:
          instance-type: C5
        outputs:
          repo:
            type: volume
        uses: git-checkout@v1
        with:
       url: https://github.com/NVlabs/stylegan2.git
      StyleGan2:
        resources:
          instance-type: P4000
        needs:
          - CloneRepo
        inputs:
          repo: CloneRepo.outputs.repo
        outputs:
          generatedFaces:
            type: dataset
            with:
              ref: demo-dataset
        uses: script@v1
        with:
          script: |-
            pip install scipy==1.3.3
            pip install requests==2.22.0
            pip install Pillow==6.2.1
            cp -R /inputs/repo /stylegan2
            cd /stylegan2
            python run_generator.py generate-images \
              --network=gdrive:networks/stylegan2-ffhq-config-f.pkl \
              --seeds=6600-6605 \
              --truncation-psi=0.5 \
              --result-dir=/outputs/generatedFaces
          image: tensorflow/tensorflow:1.14.0-gpu-py3
    ```

    Place the contents in a file named `workflow.yaml`.
5.  **Run the Workflow from the CLI**

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

From [Models](../../data/models/) to [Deployments](https://docs.paperspace.com/gradient/explore-train-deploy/deployments-preview), there's a lot more to the Gradient platform. We recommend using the Web UI to explore the primary components, including Notebooks, and basic usage of Workflows & Deployments. For more advanced non-GUI-based usage, be sure to install the [CLI](install-the-cli.md) and check out the [SDK](../../more/gradient-python-sdk-1/).
