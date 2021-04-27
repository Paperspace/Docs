# SDK Examples

In this example, we'll run through a few basic commands using the SDK.  We'll import the SDK, create a [Project](../../get-started/managing-projects/), and launch a [Workflow](../../explore-train-deploy/workflows-1/).  

{% hint style="info" %}
The SDK is bundled with the [Gradient CLI](../../get-started/quick-start/install-the-cli.md).   
{% endhint %}

{% hint style="success" %}
**NOTE:** We'll be adding a Jupyter Notebook template that you can run on your own. 
{% endhint %}

## Getting Started

```python
#Import the SDK Client from the gradient package
from gradient import sdk_client
```

```python
#create a API Key
api_key = "API_KEY_HERE"
```

```python
#Set some variables
project = "prkr4412y" # Set your project
cluster = "cl8pwu9qn" # Set your cluster
```

```python
#Set your SDK client 
deployment_client = sdk_client.DeploymentsClient(api_key)
models_client = sdk_client.ModelsClient(api_key)
jobs_client = sdk_client.JobsClient(api_key)
projects_client = ProjectsClient(api_key)
experiment_client = sdk_client.ExperimentsClient(api_key)
workflows_client = sdk_client.WorkflowsClient(api_key)

#or access them all from a single client
#client = sdk_client.SdkClient(api_key)
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

