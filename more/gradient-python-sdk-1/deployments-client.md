# Deployments Client

### Importing

```python
from gradient import gradient_deployments
api_key='YOUR_API_KEY'
```

### Create the deployment spec

You can either create a [deployment spec](../../explore-train-deploy/deployments-preview/deployment-spec.md) within your script, or import one from a YAML file on disk. For example,

```
deployment_spec = {
    'image': 'tensorflow/serving:latest-gpu',
    'port': 8501,
    'resources': {
        'replicas': 2,
        'instanceType': 'P4000'
    },
    'models': [{
        'id': model.id,
        'path': '/opt/models/'
    }],
    'env': [
        {
            'name': 'MODEL_BASE_PATH',
            'value': '/opt/models'
        }, {
            'name': 'MODEL_NAME',
            'value': 'my-tf-model'
        }
    ]
}

# or, to load from a YAML file on disk
import yaml


deployment_spec = yaml.safe_load('my_spec.yaml')
```

### Create the deployment

We'll use the `create_deployment` method to create our new deployment. Optionally, we can also pass `cluster_id=<cluster>` if you want to deploy onto a specific private cluster. You can safely omit this field if you are not using private clusters.

```
deployment = gradient_deployments.create_deployment(
    name='TensorFlow Serving Model',
    project_id='asdf1234',
    cluster_id='cluster1234',
    spec=deployment_spec,
    api_key=api_key
)
```

### Check the deployment status

We can monitor the status of our newly created deployment with the `get_deployment` function:

```
import json


deployment_info = gradient_deployments.get_deployment(
    id=deployment['id'],
    api_key=api_key
)

print(json.dumps(deployment_info, indent=4))
```

### Update the deployment

You can also modify an existing deployment at any time, and can change any of the attributes that you have specified in its deployment spec. For instance, here we are scaling the number of replicas in our deployment down to 0, and changing the instance type to a CPU-only option:

```
deployment_spec['resources']['replicas'] = 0
deployment_spec['resources']['instanceType'] = 'C4'

gradient_deployments.update_deployment(
    id=deployment['id'],
    project_id='asdf1234',
    spec=deployment_spec,
    api_key=api_key
)
```

### Delete a deployment

At any point, you can delete a deployment and remove it from the web console and from all CLI output:

```
gradient_deployments.delete_deployment(
    id=deployment['id'],
    api_key=api_key
)
```

### View and search existing deployments

We also provide a `list_deployments` method which allows you to view all active deployments. You can also optionally filter by any or all of cluster ID, project ID, and deployment name:

```
deployments = gradient_deployments.list_deployments(
    cluster_id='cluster-id-1234',
    project_id='asdf1234',
    name='TensorFlow Serving Model',
    api_key=api_key
)
```
