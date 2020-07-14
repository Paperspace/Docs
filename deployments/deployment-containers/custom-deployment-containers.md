# Custom Deployment Containers

Gradient provides the ability to use any public or private Docker container.  There are several parameters that can be used to maximize the flexibility of this managed service.  

### Parameters

{% tabs %}
{% tab title="Web UI" %}
![](../../.gitbook/assets/image%20%2883%29.png)

| Parameter | Description |
| :--- | :--- |
| Container Name | The path to the container eg `tensorflow/serving:latest-gpu` |
| Registry Username | Username used to access docker image.  This field is only required if your container originates from somewhere that is password-protected, e.g. Docker Hub. |
| Registry Password | Password used to access docker image.  This field is only required if your container originates from somewhere that is password-protected, e.g. Docker Hub. |
| Image Server | Docker image server eg https://index.docker.io/v1 |
| Port |  |
| Container Model Path | Path to the model within the container |
| Method |  |
| Container URL Path |  |
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

