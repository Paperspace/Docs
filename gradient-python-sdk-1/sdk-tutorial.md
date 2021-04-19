# End to end tutorial

In this example, we are showcasing how to use the SDK to create an end-to-end pipeline.  We'll train a model, watch the state transitions, stream the logs, inspect it's accuracy, and then deploy it as a RESTful API endpoint behind a multi-instance, load-balanced GPU cluster.  

{% hint style="info" %}
The SDK is bundled with the Gradient CLI.  You'll need the latest version which you can download by adding `--pre` when [installing \(or upgrading\) the CLI](../get-started/core-concepts/install-the-cli.md).  
{% endhint %}

{% hint style="success" %}
**NOTE:** We'll be adding a Jupyter Notebook template that you can run on your own. For now, you can download the [.ipynb](https://s3.amazonaws.com/ps.public.resources/sdk_tutorial_starter.ipynb) file here which can be imported into a Gradient Notebook instance.
{% endhint %}

## Getting Started

```python
#Import the SDK Client from the gradient package
from gradient import sdk_client, ProjectsClient
```

```python
#create a API Key
api_key = "API_KEY_HERE"
```

```python
deployment_client = sdk_client.DeploymentsClient(api_key)
models_client = sdk_client.ModelsClient(api_key)
jobs_client = sdk_client.JobsClient(api_key)
projects_client = ProjectsClient(api_key)
experiment_client = sdk_client.ExperimentsClient(api_key)

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

```python
#list experiments in the project
print(experiment_client.list([project_id])
```

## Parameters of the experiment

```python
env_variable = {
    "EPOCHS_EVAL":2,
    "TRAIN_EPOCHS":3,
    "MAX_STEPS":100,
    "EVAL_SECS":10
}

single_node_parameters = {
    "name" : "single_node_experiment-sdk",
    "project_id" : project_id,
    "command" : "python mnist.py",
    "machine_type" : "K80",
    "experiment_env": env_variable,
    "container": "tensorflow/tensorflow:1.13.1-gpu-py3",
    "workspace_url": "https://github.com/Paperspace/mnist-sample.git",
    "model_type": "Tensorflow"
}
```

## Create an experiment & view its state

```python
#create single node experiment
experiment_id = experiment_client.create_single_node(**single_node_parameters)

#get single node experiment object
from gradient import constants
#experiment state, created but not started
state = experiment_client.get(experiment_id).state
print("state: "+constants.ExperimentState.get_state_str(state))
```

## Start experiment

```python
experiment_client.start(experiment_id)

print("PAPERSPACE LINK FOR EXPERIMENT")
print("_______EXPERIMENT STARTING_____")

print()
print("https://www.paperspace.com/console/projects/"+ project_id+"/experiments/"+experiment_id)
```

## Watching the state transitions of an experiment

```python
print("Watching state of experiment")
state = "created"
while state != "running" or state != "stopped":
    new_state = constants.ExperimentState.get_state_str(experiment_client.get(experiment_id).state)
    if new_state != state:
        print("state: "+state + "  new state: "+new_state)
        state = new_state
    if state == "running":
        print("state: "+state + "  new state: "+new_state)
        break
```

## Create a log stream & print all logs for the duration of experiment

```python
#create a log stream & print all logs for the duration of experiment
log_stream = experiment_client.yield_logs(experiment_id)
print("Streaming logs of experiment")
try:
    while True:
        print(log_stream.send(None))
except:
    print("done streaming logs")
```

## Get model created by experiment

```python
#get model we just trained
model = models_client.list(experiment_id = experiment_id)

#print model
print(model)
```

## View Model Accuracy

```python
if len(model) > 0: 
    print("model accuracy: "+model[0]['accuracy'])
```

## Create a deployment from the model

```python
deploy_param = {
    "deployment_type" : "Tensorflow Serving on K8s",
    "image_url": "tensorflow/serving:latest-gpu",
    "name": "sdk_tutorial",
    "machine_type": "K80",
    "instance_count": 2,
    "model_id" : model[0].id
}
```

```python
deployment_client.create(**deploy_param)
```



