# Deployment Spec

A deployment is maintained by a spec file which is used to change the state of the deployment.

```yaml
image: lucone83/streamlit-nginx # container image used to run your deployment
containerRegistry: container-registry-name # optional reference to a private container registry
command: # optional command to override the container image's default command
  - my
  - command
port: 8080 # local container port that your service is running on
env: # environment variables that are applied at run time
  - name: ENV
    value: VAR
models:
  - id: model-handle # the handle of a model from the Gradient Model Registry
    path: /opt/models # the local filepath you want to sync it to inside your deployment
repositories:
  dataset: dataset-ref # the ID of the dataset you want to sync the repository with
  mountPath: /opt/repos # the  local filepath you want to sync the repos to inside your deployment
  repositories:
    - url: https://github.com/tensorflow/serving.git # the URL of the repository
      name: tf-serving # the folder name you want to clone the repo into
      username: example # optionally, the username to authenticate to the repo with
      password: SECRET:secret_name # optionally, the Gradient Secret containing the password for your Git user
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

### Cloning Repositories into a Deployment

If you don't want to package everything into a Docker container, you can also clone any one or more Git repositories into your Deployment at runtime. To do this, just supply the optional `repositories` configuration in your deployment spec, and specify:

* the dataset ID you want to use to sync the repositories into;
* the folder that you want to access your repositories from within the Deployment; and
* the URL for one or more Git repositories that you want to clone

Note that if you are using a private Git repository, you can configure authenticated access by also supplying the optional `username` and `password` parameters. The password field will need to reference a [Gradient Secret](../../get-started/managing-projects/using-secrets.md) and should not contain the plaintext password itself.

You must also have already created a [Gradient Dataset](../../data/data-overview/private-datasets-repository/) to use this feature. We clone your repository into a Dataset for local storage and access within the cluster by your Deployment and are not able to automatically create one for you at this time.

For example, let's say that I want to clone two repositories, one that is public, and one that is private and requires a username and password. I might use a spec like the following:

```
image: ubuntu:20.04
port: 8501
resources:
  replicas: 1
  instanceType: C4
repositories:
  dataset: dstflhstfexl6w3
  mountPath: /opt/repositories
  repositories:
    - url: https://github.com/tensorflow/serving.git
      name: tf-serving
    - url: https://github.com/paperspace/ml-private.git
      name: paperspace-ml
      username: paperspace-user
      password: SECRET:paperspace-github-token
```

Once this completes, I will have access to the TensorFlow Serving repository at `/opt/repos/tf-serving`, and to a repo of private ML code at `/opt/repos/paperspace-ml`.

### Container Registry integration

Private Docker images can be used by referencing your Container Registry which contains credentials to access that image.

To configure a Container Registry, follow this short [guide](../../data/containers.md).

Once configured, we add a `containerRegistry` parameter to our deployment spec and specify the name of the Container Registry.

```yaml
image: paperspace/ml_server
containerRegistry: dockerhub-prod
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
