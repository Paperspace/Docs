# Custom Deployment Containers

Gradient provides the ability to use any public or private Docker container.  There are several parameters that can be used to maximize the flexibility of this managed service.  

### Parameters

{% tabs %}
{% tab title="Web UI" %}
![](../../.gitbook/assets/image%20%2861%29.png)
{% endtab %}

{% tab title="CLI" %}
Here is a list of parameters you can pass in via the CLI:

```bash
Usage: gradient deployments create [OPTIONS]

  Create new deployment

Options:
  --deploymentType [TFServing|ONNX|Custom|Flask|TensorRT]
                                  Model deployment type  [required]
  --modelId TEXT                  ID of a trained model  [required]
  --name TEXT                     Human-friendly name for new model deployment
                                  [required]
  --machineType TEXT              Type of machine for new deployment
                                  [required]
  --imageUrl TEXT                 Docker image for model serving
                                  [required]
  --instanceCount INTEGER         Number of machine instances
                                  [required]
  --containerModelPath TEXT       Container model path
  --imageUsername TEXT            Username used to access docker image
  --imagePassword TEXT            Password used to access docker image
  --imageServer TEXT              Docker image server
  --containerUrlPath TEXT         Container URL path
  --endpointUrlPath TEXT          Endpoint URL path
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
```
{% endtab %}
{% endtabs %}

