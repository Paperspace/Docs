# Deployments Client

### Importing

```python
from gradient import DeploymentsClient
api_key='YOUR_API_KEY'

deployment_client = DeploymentsClient(api_key)
```

### Select model to deploy

Get a model to deploy by either selecting experiment output or filtering based on some criteria from a project

```text
model = models_client.list(experiment_id = experiment_id)[0]
```

### Deployment parameters

```text
deployment_param = {
    "deployment_type" : "Tensorflow Serving on K8s",
    "image_url": "tensorflow/serving:latest-gpu",
    "name": "sdk_tutorial",
    "machine_type": "K80",
    "instance_count": 2,
    "model_id" : model.id
}
```

### Create the deployment

```text
deployment_id = deployment_client.create(**deploy_param)
```

### Start the deployment

```text
deployment_client.start(deployment_id)
```

### Stop a deployment

```text
deployment_client.stop(deployment_id)
```

### 

