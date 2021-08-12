# Managing Deployments

{% hint style="info" %}
View the full CLI/SDK Docs for **Deployments** here [https://paperspace.github.io/gradient-cli/gradient.cli.html\#gradient-deployments](https://paperspace.github.io/gradient-cli/gradient.cli.html#gradient-deployments)
{% endhint %}

## Create a Deployment

{% tabs %}
{% tab title="Web UI" %}
### The Create Deployment flow

To create a Deployment via the UI, there are two pathways to start the Create Deployment flow: **a\)** from a Model on the **Models** page; **b\)** from the **Deployments** page. Both of these pathways are shown below, after which we will step through the Create Deployment flow.

#### a\) From the Models page:

1. Navigate to your list of trained Models by clicking **Models** in the side nav.
2. Find the model you want to deploy, and click **Deploy Model**.

![A Model shown in the &quot;cards&quot; view on the Models page](../../../.gitbook/assets/deploy-model-from-model.png)

#### b\) From the Deployments page:

1. Navigate to your list of Deployments by clicking **Deployments** in the side nav.
2. Click **Create Deployment +**.

![](../../../.gitbook/assets/create-deployment-from-deployments.png)

### Using the Create Deployment flow

Now that you've started the Create Deployment flow, let's walk through the various options and deploy your Model!

#### Choose a Model

If you started the flow via the Models page \(pathway **a** above\), you'll skip this step since you've already chosen a Model to deploy.

If you started the flow via the Deployments page \(pathway **b** above\), you have the option to choose a Model by clicking the Model selector dropdown and selecting the Model you want to deploy. 

![](../../../.gitbook/assets/create-deployment-header.png)

#### Choose a Container

Select the base container that will support your trained model to run it as a continuous web service. As both CPU & GPU serving are available, be sure to select the container corresponding to your selected machine type and what your Model was optimized for.

![Recommended container options shown with Tensorflow/serving selected](../../../.gitbook/assets/screen-shot-2019-12-31-at-1.59.11-pm.png)

#### Choose an instance type

Select the GPU or CPU machine type to run your Deployment.

![If you are using Gradient Enterprise, you&apos;ll want to select from among My Private Clusters](../../../.gitbook/assets/screen-shot-2019-12-31-at-1.59.02-pm.png)

### Additional Input Parameters

#### Name

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-2.06.14-pm.png)

#### **Instance Count**

Select the number of instances to run the Deployment on.  Below we chose 3, meaning there will be 3x K80 GPU instances backing this Deployment. Automatic load balancing is provided for all multi-instance deployments.

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-2.10.15-pm.png)

#### **Command**

If applicable, choose a command to run at container launch.

{% hint style="info" %}
**Note:** for the Tensorflow/serving base container used here, the command to run the Deployment is unnecessary and thus disabled. This option can be changed when choosing a different base image to deploy on_._
{% endhint %}

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-2.06.32-pm.png)

#### Creative Active Deployment

**Create Active Deployment** \(selected by default\) means that the Deployment will be created and then automatically run:

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-2.15.49-pm.png)

Alternately, if you don't want your Deployment to run automatically after it is created, you can click toggle **Create Inactive Deployment**:

![](../../../.gitbook/assets/screen-shot-2019-06-24-at-8.17.48-pm.png)

{% hint style="info" %}
**Note:** You are only charged for Deployments when they are running.
{% endhint %}

#### Enable Basic Authentication

Since your Deployment will run as a continuous web service on the public internet, you may wish to require basic authentication on any requests to it. If so, be sure that **Enable Basic Authentication** is toggled _on_ and then enter a **username** and **password**:

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-2.37.18-pm.png)

Finally, now that your Deployment is configured, click **Create Deployment** to create it:

![](../../../.gitbook/assets/create%20%282%29.png)

#### Environment variables

When running a custom container you can set environment variables for your deployment.

![](../../../.gitbook/assets/image%20%2879%29%20%283%29%20%283%29%20%283%29%20%283%29.png)

Enter them as a 1 level deep JSON object. Environment variables can reference secrets stored on your project, team or cluster using the subsitution syntax: `secret:my-secret` for example:

```text
{"DB_CONNECTION_STRING": "secret:MY_DB_CONNECTION", "MY_APP_LOG_LEVEL": "debug"}
```
{% endtab %}

{% tab title="CLI" %}
Use the `create` subcommand and specify all of the following parameters you need to deploy your model.  Here's a sample command to create the same Deployment as you could do from the UI:

```bash
gradient deployments create \
    --deploymentType TFServing \
    --modelId <your-model-id> \
    --name "Sample Model"
    --machineType K80
    --imageUrl tensorflow/serving:latest-gpu
    --instanceCount 2
```

To obtain your Model ID, you can use the command `gradient models list` and copy the target Model ID from your available Models.  
  
The full set of options for deployments: 

```text
  --deploymentType [TFServing|ONNX|Custom|Flask|TensorRT]
                                  Model deployment type  [required]
  --projectId TEXT                Project ID
  --modelId TEXT                  ID of a trained model
  --name TEXT                     Human-friendly name for new model deployment
                                  [required]

  --machineType TEXT              Type of machine for new deployment
                                  [required]

  --imageUrl TEXT                 Docker image for model serving
                                  [required]

  --instanceCount INTEGER         Number of machine instances
                                  [required]

  --command TEXT                  Deployment command
  --containerModelPath TEXT       Container model path
  --imageUsername TEXT            Username used to access docker image
  --imagePassword TEXT            Password used to access docker image
  --imageServer TEXT              Docker image server
  --containerUrlPath TEXT         Container URL path
  --method TEXT                   Method prefix - default to '/' - If TFServing REST method prefix is ':'
  --dockerArgs JSON_STRING        JSON-style list of docker args
  --env JSON_STRING               JSON-style environmental variables map
  --apiType TEXT                  Type of API - REST or GRPC, defaults to REST
  --ports TEXT                    Expose ports: Takes a single value eg 80
  --clusterId TEXT                Cluster ID
  --authUsername TEXT             Username
  --authPassword TEXT             Password
  --auth                          Generate username and password. Mutually
                                  exclusive with --authUsername and
                                  --authPassword

  --tag TEXT                      One or many tags that you want to add to
                                  model deployment job

  --tags TEXT                     Separated by comma tags that you want add to
                                  model deployment job

  --workspace TEXT                Path to workspace directory, archive, S3 or
                                  git repository

  --workspaceRef TEXT             Git commit hash, branch name or tag
  --workspaceUsername TEXT        Workspace username
  --workspacePassword TEXT        Workspace password
  --minInstanceCount TEXT         Minimal instance count
  --maxInstanceCount TEXT         Maximal instance count
  --scaleCooldownPeriod TEXT      Scale cooldown period
  --metric TEXT                   Autoscaling metrics. Example:
                                  my_metric/targetAverage:21.37

  --resource TEXT                 Autoscaling resources. Example:
                                  cpu/target:60
```

Sometimes, a user will want to do inference with a custom model using a custom container. An example of this is building a Flask or Streamlit container which will use the model trained on Gradient to do inference but also expose a custom dashboard for the team to use to consume the predictions for making business decisions. This is accomplished by specifying the modelType to be "Custom" & passing in the information for the custom container. 
{% endtab %}
{% endtabs %}

## View, Start, & Stop a Deployment

{% tabs %}
{% tab title="Web UI" %}
Since Deployments are continuous web services, they can be in multiple states, including _Provisioning_, _Provisioned_, _Running_, _Stopped_, and _Error_.

Navigate to the **Deployments** page in the side nav to see your list of Deployments:

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-3.48.12-pm.png)

Each Deployment has: a **Name** and a unique **ID**; links to its associated **Experiment** and **Model** \(by ID\) that it was created from; its **Container Type; Date Created; Status;** and **Actions** you can perform.

To start a _Stopped_ Deployment, click **Start** from among that Deployment's **Actions**. The Status will change to _Provisioning_ and, if all goes smoothly, will soon say _Running_. Learn more about [Deployment States](deployment-states.md).

Click the Deployment's row to show its details:

![](../../../.gitbook/assets/screen-shot-2019-06-24-at-8.37.24-pm.png)

Each Deployment has its own unique RESTful API. Inference can be performed via the shown endpoint: `https://services.paperspace.io/model-serving/<your-model-id>:predict`.  The number of running instances and the instance count are visible as well.

Congrats, you've created a Deployment and can perform inference!

[Learn more about a Deployment's RESTful API here](a-deployed-models-api-endpoint/deployment-restful-api-tfserving.md).
{% endtab %}

{% tab title="CLI" %}
## List Deployments

To list your Deployments with optional filtering, use the `list` subcommand:

```text
gradient deployments list 
```

**Options:**

```bash
  --state [BUILDING|PROVISIONING|STARTING|RUNNING|STOPPING|STOPPED|ERROR]
                                  Filter by deployment state
  --projectId TEXT                Use to filter by project ID
  --modelId TEXT                  Use to filter by model ID
  --apiKey TEXT                   API key to use this time only
  --optionsFile PATH              Path to YAML file with predefined options
  --createOptionsFile PATH        Generate template options file
  --help                          Show this message and exit.
```

For example, to view all running Deployments in your team, run:

```bash
gradient deployments list --state RUNNING
```

## Start a Deployment

To start a previously created but Stopped deployment by ID, use the `start` subcommand:

```bash
gradient deployments start --id <your-deployment-id>
```

## Stop a Deployment

To stop a _Running_ Deployment by ID, use the `stop` subcommand:

```bash
gradient deployments stop --id <your-deployment-id>

```
{% endtab %}
{% endtabs %}

## Edit a Deployment

{% tabs %}
{% tab title="Web UI" %}
You can edit a Deployment's attributes, such as the underlying model, the Deployment's name, instance count, etc.

To edit a Deployment, navigate to the **Deployments** page, find the Deployment you want to edit, and click **Edit** in the Actions column:

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-2.44.20-pm.png)

This will launch the Edit Deployment flow, which is nearly the same as the Create Deployment flow. The differences are that the Edit Deployment flow will display the **Deployment ID**, the **Deployment Endpoint**, and will always allow you to **Choose a Model**; and it will _not_ display the **Create Active Deployment** toggle. \(If you want to edit and start a stopped Deployment, save your changes and then click **Start** back on the Deployments page.\)

![](../../../.gitbook/assets/screen-shot-2019-12-31-at-3.08.58-pm.png)

Besides those differences, you can edit any of the other values of your Deployment just like you did in the Create Deployment flow.

When you are done and want to save your changes, click **Edit Deployment** at the bottom:

![](../../../.gitbook/assets/edit.png)
{% endtab %}

{% tab title="CLI" %}
You can edit a Deployment's attributes, such as the underlying model, the Deployment's name, instance count, etc.

To update a Deployment, use the `update` subcommand:

```bash
gradient deployments update --id <your-deployment-id>
```

All Deployment options can be updated with this command: 

```bash
Usage: gradient deployments update [OPTIONS]

  Modify existing deployment

Options:
  --id TEXT                       ID of existing deployment
                                  [required]

  --deploymentType [TFServing|ONNX|Custom|Flask|TensorRT]
                                  Model deployment type
  --projectId TEXT                Project ID
  --modelId TEXT                  ID of a trained model
  --name TEXT                     Human-friendly name for new model deployment
  --machineType TEXT              Type of machine for new deployment
  --imageUrl TEXT                 Docker image for model serving
  --instanceCount INTEGER         Number of machine instances
  --command TEXT                  Deployment command
  --containerModelPath TEXT       Container model path
  --imageUsername TEXT            Username used to access docker image
  --imagePassword TEXT            Password used to access docker image
  --imageServer TEXT              Docker image server
  --containerUrlPath TEXT         Container URL path
  --method TEXT                   Method
  --dockerArgs JSON_STRING        JSON-style list of docker args
  --env JSON_STRING               JSON-style environmental variables map
  --apiType TEXT                  Type of API
  --ports TEXT                    Ports
  --authUsername TEXT             Username
  --authPassword TEXT             Password
  --clusterId TEXT                Cluster ID
  --workspace TEXT                Path to workspace directory, archive, S3 or
                                  git repository

  --workspaceRef TEXT             Git commit hash, branch name or tag
  --workspaceUsername <username>  Workspace username
  --workspacePassword TEXT        Workspace password
  --minInstanceCount TEXT         Minimal instance count
  --maxInstanceCount TEXT         Maximal instance count
  --scaleCooldownPeriod TEXT      Scale cooldown period
  --metric TEXT                   Autoscaling metrics. Example:
                                  my_metric/targetAverage:21.37

  --resource TEXT                 Autoscaling resources. Example:
                                  cpu/target:60

  --apiKey TEXT                   API key to use this time only
  --optionsFile PATH              Path to YAML file with predefined options
  --createOptionsFile PATH        Generate template options file
  --help                          Show this message and exit.

```
{% endtab %}
{% endtabs %}

## Secure Deployment with Basic HTTPS authentication

The client sends the user name and password as unencrypted base64 encoded text.  

Most web browsers will display a login dialog when this response is received, allowing the user to enter a username and password. 

{% tabs %}
{% tab title="GUI" %}
![](../../../.gitbook/assets/screenshot-2020-02-25-at-17.34.11.png)

To add HTTP authentication to deployment in GUI - at the bottom of the creation page you have to check _"Enable Basic Authentication"_
{% endtab %}

{% tab title="CLI" %}
To secure a deployment with HTTP authentication you have to pass 

```text
--authUsername 'testuser' 
--authPassword 'test' 
```

Example command:

```text
gradient deployments create 
--deploymentType TFServing 
--name "authtest" 
--modelId <model id> 
--authUsername 'testuser' 
--authPassword 'test' 
--machineType c5.xlarge 
--clusterId clu7jqg9j 
--imageUrl 'tensorflow/serving:latest' 
--instanceCount 1
```
{% endtab %}
{% endtabs %}









