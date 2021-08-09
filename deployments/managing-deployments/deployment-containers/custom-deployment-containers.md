# Custom Deployment Containers

Gradient provides the ability to use any public or private Docker container.  There are several parameters that can be used to maximize the flexibility of this managed service.  

### Parameters

{% tabs %}
{% tab title="Web UI" %}
![](../../../.gitbook/assets/image%20%2894%29.png)

| Parameter | Description |
| :--- | :--- |
| Container Name | The path to the container eg `tensorflow/serving:latest-gpu` |
| Registry Username | Username used to access docker image.  This field is only required if your container originates from somewhere that is password-protected, e.g. Docker Hub. |
| Registry Password | Password used to access docker image.  This field is only required if your container originates from somewhere that is password-protected, e.g. Docker Hub. |
| Image Server | Docker image server eg https://index.docker.io/v1 |
| Container Model Path | Path to the model within the container |
| Method | Method |
| Port | Ports to open up eg 80:8080 |
| Container URL Path | Docker image for model serving |
| Endpoint URL Path |  |
| Docker Arguments \(CSV\) |  |
| Environment Variables \(JSON\) |  |
{% endtab %}

{% tab title="CLI" %}
Here is a list of parameters you can pass in via the CLI:

```bash
Usage: gradient deployments create [OPTIONS]

  Create new deployment

Options:
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
  --method TEXT                   Method
  --dockerArgs JSON_STRING        JSON-style list of docker args
  --env JSON_STRING               JSON-style environmental variables map
  --apiType TEXT                  Type of API
  --ports TEXT                    Ports
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

  --apiKey TEXT                   API key to use this time only
  --optionsFile PATH              Path to YAML file with predefined options
  --createOptionsFile PATH        Generate template options file
  --help                          Show this message and exit.

```
{% endtab %}
{% endtabs %}

### Running Custom Container from Private Registry

To run a custom container on a private registry, you need to specify the following fields:

{% tabs %}
{% tab title="Web UI" %}
Populate the Container Name, Image Server, Registry Username, Registry Password fields \(plus any other optional fields\) to pull a container from your private registry. 

![](../../../.gitbook/assets/image%20%2893%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29.png)
{% endtab %}

{% tab title="CLI" %}
```bash
  --imageUrl TEXT                 Docker image for model serving
                                  [required]
  --imageUsername TEXT            Username used to access docker image
  --imagePassword TEXT            Password used to access docker image
  --imageServer TEXT              Docker image server
```
{% endtab %}
{% endtabs %}

### Example of running a flask server using the deployments CLI

```text
gradient deployments create 
--deploymentType Custom 
-name "flaskserver" 
--machineType c5.xlarge 
--imageUrl tiangolo/uwsgi-nginx-flask 
--instanceCount 1 
--clusterId <someCluster>
--port 80:8080
```



