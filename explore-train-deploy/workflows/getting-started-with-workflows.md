# Getting Started with Workflows

The following sections cover creating and running workflows, and authoring new workflow yaml specs. If you have never run a workflow before we recommend you step through the workflows demo in the [quick-start guide](https://docs.paperspace.com/gradient/get-started/quick-start#create-a-project) then return here for more details.

## Create a Workflow

{% hint style="info" %}
View the full CLI/SDK Docs for **Workflows** here [https://paperspace.github.io/gradient-cli/gradient.cli.html\#gradient-workflows](https://paperspace.github.io/gradient-cli/gradient.cli.html#gradient-workflows)
{% endhint %}

1. Make sure you have the latest version of the [Gradient CLI](../../get-started/quick-start/install-the-cli.md)
2. Create a [Gradient Project](../../get-started/managing-projects/) and [grab your project ID](../../get-started/managing-projects/#get-your-projects-id)
3. Create your first workflow using the Gradient CLI

```bash
gradient workflows create --name <my-workflow-name> --projectId <project-id>
```

The command will return an ID for the workflow, for example, `7634c165-5034-4f49-95fa-005fc0e7970b`.

## Create a Workflow Spec

Create a workflow spec in [yaml](https://yaml.org) using a text editor. Note: even though YAML and JSON are closely releated, Gradient workflows need to be formatted as YAML and not JSON. Below is an example of a valid **workflow.yaml** spec. You will learn more about writing workflow specs on the following pages.

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

## Create Datasets for the Workflow

Datasets referenced in the workflow spec need to be created before running the workflow for the first time. On subsequent runs of the workflow the datasets will be used again, but different **dataset versions** will be created for each output dataset. For more information about Datasets see [Versioned Data](https://docs.paperspace.com/gradient/data/data-overview#versioned-data).

The above workflow creates a new output dataset version in the dataset named `demo-dataset`. So before running this workflow make sure a dataset with that name already exists. You can run this command to list your datasets: `gradient datasets list`.

If you completed the worflows demo in the [quick-start guide](https://docs.paperspace.com/gradient/get-started/quick-start#create-a-project) you will already have a dataset with this name. If not you can create it using the following commands.

First get a list of storage providers that are already part of your account. You should have at least one called **Gradient Managed**.

```bash
gradient storageProviders list
+------------------+-----------------+------+------------------------------------------+
| Name             | ID              | Type | Config                                   |
+------------------+-----------------+------+------------------------------------------+
| Gradient Managed | splXXXXXXXXXXXX | s3   | accessKey: XXXXXXXXXXXXXXXXXXXX          |
|                  |                 |      | bucket: XXXXXXXXX                        |
|                  |                 |      | endpoint: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX |
|                  |                 |      | secretAccessKey: ********                |
+------------------+-----------------+------+------------------------------------------+
```

Then create a dataset named **demo-dataset** using the **Gradient Managed** storage provider ID:

```bash
gradient datasets create \
  --name demo-dataset \
  --storageProviderId splXXXXXXXXXXXX
```

## Run the Workflow

Run the workflow with the specified workflow spec file and the **`workflow-id`** from the previously created workflow. \(You can also get a list of workflows by running `gradient workflows list`.\)

```bash
gradient workflows run \
    --id <worklow-id> \ 
    --path ./workflow.yaml
```

A workflow can be run multiple times, each with the same or a different workflow yaml spec. The workflow spec is recorded as part of the workflow run so you can distinguish different runs.

The next sections cover the syntax for authoring new workflow specs, inputs and outputs to workflow steps, and various workflow actions.

