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

You can also automatically pull in any models that you have registered through the Gradient Model Registry at runtime. To do this, we just add a `models` parameter to our deployment spec where we can specify the model(s) we want to pull in by their ID, and optionally also the filepath inside our deployed container where we want to mount them into. If the path is not specified, it will default to `/opt/models`.

```yaml
image: tensorflow/serving
port: 8501
models:
  - id: model-id
    path: /opt/models
env:
  - name: MODEL_BASE_PATH
    value: /opt/models
  - name: MODEL_NAME
    value: my-tf-model
resources:
  replicas: 1
  instanceType: C4
```
