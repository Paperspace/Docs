# SDK Examples

In this example, we'll run through a few basic commands using the SDK.  We'll import the SDK, create a [Project](../../get-started/managing-projects/), and launch a [Workflow](../../explore-train-deploy/workflows/). &#x20;

{% hint style="info" %}
The SDK is bundled with the [Gradient CLI](../../get-started/quick-start/install-the-cli.md).  &#x20;
{% endhint %}

{% hint style="success" %}
**NOTE: **We'll be adding a Jupyter Notebook template that you can run on your own.&#x20;
{% endhint %}

## Getting Started

This assumes that you have the environment variable `PAPERSPACE_API_KEY` set to your api key. If you are using a Paperspace environment it is recommend to [use a secret to pass it to your workload](https://docs.paperspace.com/gradient/get-started/managing-projects/storing-an-api-key-as-a-secret). If you are using an interactive environment use the `gradient apiKey` command to securely configure your api key.

```python
#Import the SDK Client from the gradient package
from gradient import sdk_client
```

```python
#Set some variables
project = "prkr4412y" # Set your project
cluster = "cl8pwu9qn" # Set your cluster
```

```python
#Set your SDK client 
deployment_client = sdk_client.DeploymentsClient()
models_client = sdk_client.ModelsClient()
jobs_client = sdk_client.JobsClient()
projects_client = ProjectsClient()
experiment_client = sdk_client.ExperimentsClient()
workflows_client = sdk_client.WorkflowsClient()

#or access them all from a single client
#client = sdk_client.SdkClient()
```

## Print list of projects

```python
projects_list = projects_client.list()
for project in projects_list:
       print("project_id: "+project.id +" project_name: "+ project.name)
```

## Create project

```python
#create a new project
project_id = projects_client.create("sample_tutorials")
print("project_id: "+proj_id)
```

## Launch a Workflow

Grab your Workflow ID

```python
workflows = workflows_client.list( project_id=project)
```

Run the Workflow

```python
spec_path = "./sample.yaml"

yaml_spec = open(spec_path, 'r')
spec = yaml.safe_load(yaml_spec)


workflow_param = {
    "workflow_id" : "08676d5c-9873-4d24-a5d4-1fcc92218379",
    "spec": spec,
    "cluster_id" : cluster,
    "inputs": None
}

run_id = workflows_client.run_workflow(**workflow_param)
```
