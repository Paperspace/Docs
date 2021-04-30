# Understanding Inputs & Outputs

A Gradient Workflow is composed of a series of steps. These steps specify how to orchestrate computational tasks. Each step can communicate with other steps through what are known as `inputs`  and `outputs`.

![](../../.gitbook/assets/image%20%2810%29.png)

There are three types of inputs and outputs. Understanding how these function will help you craft concise and elegant Workflows.

* Datasets
* Volumes
* Strings

## Datasets

The dataset type leverages the Gradient platform native [dataset](../../data/data-overview/) primitive. Information stored within datasets is not limited to any single type of data. In fact, a generic dataset can include anything from pretrained models to generated images to configuration files. Inherent to datasets is the notion of versions. Workflows can consume and produce new datasets as well as tag new versions of existing datasets.

Scenario 1: Consuming a dataset that already exists within Gradient

```yaml
inputs:
    my-dataset: 
        type: dataset
        with:
            id: my-dataset-id
```

Scenario 2: Generating a new dataset version from a Workflow step

```yaml
my-job:
  uses: container@v1
  with:
    args:
      - bash
      - '-c'
      - cp -R /my-trained-model /outputs/my-dataset
    image: bash:5
  outputs:
    my-dataset:
      type: dataset
      with:
        id: my-dataset-id
```

## Volumes

Unlike, e.g. GitHub Actions, it is likely that multiple Gradient Steps/Actions will execute on multiple compute nodes. To facilitate the passing of data between these nodes, Gradient Actions exposes the notion of volumes and volume passing.

Volumes enable actions such as the [@git-checkout action](gradient-actions.md#git-checkout).

```yaml
inputs:
    my-volume-name:
        type: volume
```

## Strings

In some cases, you may need to pass a single value between Workflow steps. The string type makes this possible.

Scenario 1: Passing a generated model ID to a subsequent [Deployment](../deployments/) step

{% hint style="info" %}
NOTE: There is no native Gradient Actions for Model Deployments today. Instead, you can use the [Gradient SDK](../../more/gradient-python-sdk-1/) to create and manage your inference endpoints.
{% endhint %}

```yaml
DeployModel:
    resources:
      instance-type: P4000
    needs:
      - UploadModel
    inputs:
      model-id: UploadModel.outputs.model-id
    uses: container@v1
    with:
      args:
        - bash
        - "-c"
        - >-
            printenv && gradient deployments create \
            --deploymentType TFServing \
            --modelId $(cat inputs/model-id) \
            --name "Sample Model"
            --machineType K80
            --imageUrl tensorflow/serving:latest-gpu
            --instanceCount 2
            --apiKey ${apiKey}
      image: paperspace/gradient-sdk
```

More sample code coming soon!

