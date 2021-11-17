# Deployment Spec

A deployment is maintained by a spec file which is used to change the state of the deployment.

```yaml
image: lucone83/streamlit-nginx # container image used to run your deployment
command: # optional command to override the container image's default command
  - my
  - command
port: 8080 # local container port that your service is running on
env: # environment variables that are applied at run time
  - name: ENV
    value: VAR
resources:
  replicas: 1 # number of replicas used for your deployment
  instanceType: C4 # instance type that your deployment will run on
```

### Model integration

```yaml
image: tensorflow/serving
port: 8501
models:
  - id: model-id
    path: "/opt/models/my-tf-model"
command:
  - "--model_base_path"
  - "/opt/models"
  - "--model-name"
  - "my-tf-model"
resources:
  replicas: 1
  instanceType: C4
```
