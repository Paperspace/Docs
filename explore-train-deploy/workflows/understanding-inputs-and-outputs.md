# Understanding Inputs & Outputs

A Gradient Workflow is composed of a series of steps. These steps specify how to orchestrate computational tasks. Each step can communicate with other steps through what are known as `inputs` and `outputs`.

![](../../.gitbook/assets/image%20%2810%29.png)

There are three types of inputs and outputs. Understanding how these function will help you craft concise and elegant Workflows.

* Datasets
* Volumes
* Strings

## Datasets

The dataset type leverages the Gradient platform native [dataset](../../data/data-overview/) primitive. Information stored within datasets is not limited to any single type of data. In fact, a generic dataset can include anything from pretrained models to generated images to configuration files. Inherent to datasets is the notion of versions. Workflows can consume and produce new dataset versions as well as tag new versions of existing datasets. Note: datasets must be defined in advance of being referenced in a workflow. See the [dataset](../../data/data-overview/) documentation for more info.

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

Volumes enable actions such as the [@git-checkout action](gradient-actions.md#git-checkout).  Volumes can be defined as input volumes or output volumes or both.  Volumes currently need to be specified in jobs, but in the future they will also be specified as workflow resources.  Here is a simple output volume:

```yaml
    outputs:
      my-volume:
        type: volume
```

In this example a volume is first created as an output and then used as an input in a subsequent job step:

```yaml
defaults:
  resources:
    instance-type: P4000

jobs:
  job1:
    uses: container@v1
    with:
      args:
      - bash
      - -c
      - echo hello > /outputs/my-volume/testfile1; echo "wrote testfile1 to volume"
      image: bash
    outputs:
      my-volume:
        type: volume
  job2:
    needs:
    - job1
    uses: container@v1
    with:
      args:
      - bash
      - -c
      - cat /inputs/my-volume/testfile1
      image: bash
    inputs:
      my-volume: job1.outputs.my-volume
```

The same volume can be used as both an input and an output for cases where you want to modify the contents of an existing volume and pass it to a subsequent step.
To do this use the same name for the volume in both the inputs and outputs section of the job:

```yaml
    inputs:
      my-volume: setup-job.outputs.my-volume
    outputs:
      my-volume:
        type: volume
```

Note: currently there is only one unique volume per job. If more than one volume is define in a job they will all refer to the same underlying storage. (We plan to remove this restriction in a future version.)

## Strings

In some cases, you may need to pass a single value between Workflow steps. The string type makes this possible.

Scenario 1: Passing a string from as a workflow-level input

```yaml
inputs:
  my-string:
    type: string
    with:
      value: "my string value"

jobs:
  job-1:
    resources:
      instance-type: P4000
    uses: container@v1
    with:
      args:
      - bash
      - -c
      - cat /inputs/my-string
      image: bash:5
    inputs:
      my-string: workflow.inputs.my-string
```
        
Scenario 2: Passing a string between job steps

```yaml
defaults:
  resources:
    instance-type: P4000

jobs:
  job-1:
    uses: container@v1
    with:
      args:
      - bash
      - -c
      - echo "string output from job-1" > /outputs/my-string; echo job-1 finished
      image: bash:5
    outputs:
      my-string:
        type: string
  job-2:
    uses: container@v1
    with:
      args:
      - bash
      - -c
      - cat /inputs/my-string
      image: bash:5
    needs:
     - job-1
    inputs:
      my-string: job-1.outputs.my-string
```

Scenario 3: Creating a model from a dataset and passing the model ID as a string to a [Deployment](../deployments/) step

{% hint style="info" %}
NOTE: There is no native Gradient Actions for Model Deployments today. Instead, you can use the [Gradient SDK](../../more/gradient-python-sdk-1/) to create and manage your inference endpoints.
{% endhint %}

To run this example you will need to
a) create a dataset named test-model and upload your model files to it,
b) define a secret named MY_API_KEY with your gradient-cli api-key,
c) substitute your clusterId in the deployment create step.

```yaml
defaults:
  resources:
    instance-type: P4000

jobs:
  UploadModel:
    uses: create-model@v1
    with:
      name: my-model
      type: Tensorflow
    inputs:
      model:
        type: dataset
        with:
          id: test-model
    outputs:
      model-id:
        type: string
  DeployModel:
    needs:
    - UploadModel
    inputs:
      model-id: UploadModel.outputs.model-id
    env:
      PAPERSPACE_API_KEY: secret:MY_API_KEY
    uses: container@v1
    with:
      command: bash
      args:
      - -c
      - >-
       gradient deployments create
       --clusterId cl1234567
       --deploymentType TFServing
       --modelId $(cat inputs/model-id)
       --name "Sample Model"
       --machineType P4000
       --imageUrl tensorflow/serving:latest-gpu
       --instanceCount 2
      image: paperspace/gradient-sdk
```
