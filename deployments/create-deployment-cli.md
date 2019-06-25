# Create a Deployment via the CLI

Make sure you have the CLI installed as outlined here: [https://docs.paperspace.com/gradient/get-started/install-the-cli](https://docs.paperspace.com/gradient/get-started/install-the-cli). 

The gradient cli contains the following options for deployments: create, list, start, stop. Get access to this by typing the following. You can always get help for a particular command by appending --help

```text
gradient deployments
```

![](../.gitbook/assets/screen-shot-2019-06-24-at-10.57.30-pm.png)

#### gradient deployments create

This creates a brand new deployment, requiring you to already have a model saved via running an experiment. Specify all of the following parameters \(the deployment type, the base image, the name, the machine type, the container image for serving along with the instance count.  

![](../.gitbook/assets/screen-shot-2019-06-24-at-10.57.59-pm.png)

A sample workflow to create the same deployment as in the UI example would be to run the following once you have your api key saved

```text
#get list of models & select 1 for deployment
gradient models list
```

```text
gradient deployments create \
    --deploymentType TFServing \
    --modelId [your-model-id] \
    --name "Sample Model"
    --machineType K80
    --imageUrl tensorflow/serving:latest-gpu
    --instanceCount 2
```

#### gradient deployments list

List deployments with optional filtering

![](../.gitbook/assets/screen-shot-2019-06-25-at-2.59.35-pm.png)

For example, to view all running deployments in your team

```text
gradient list --state RUNNING
```

#### gradient deployments start

Start a previously created but inactive deployment by id

![](../.gitbook/assets/screen-shot-2019-06-24-at-10.58.55-pm.png)

```text
gradient deployments start --id [deployment-id]
```

#### gradient deployments stop

Stop a active deployment by id

![](../.gitbook/assets/screen-shot-2019-06-24-at-10.59.08-pm.png)

```text
gradient deployments stop --id [deployment-id]
```

