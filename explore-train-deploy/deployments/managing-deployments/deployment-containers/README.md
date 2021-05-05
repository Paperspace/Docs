# Deployment Containers

## Base Containers

When you launch a Deployment, it runs inside a Docker container \(often referred to as a runtime\). Any Docker image hosted in a public or private container registry can be used as the Deployment's runtime. Additionally, Gradient includes several popular runtimes out of the box:

### Popular Containers

| Name | Description | Container Tag | URL |
| :--- | :--- | :--- | :--- |
| _**TensorFlow**_             | TensorFlow Serving | `tensorflow/serving:latest-gpu` | [DockerHub](https://hub.docker.com/r/tensorflow/serving) |
| _**ONNX**_ | Based on the official ONNX community project | `paperspace/onnx` | [DockerHub](https://hub.docker.com/r/paperspace/onnx) |
| _**TensorRT**_ | NVIDIA's optimized runtime | `paperspace/tensorrt` | \*\*\*\*[DockerHub](https://hub.docker.com/r/paperspace/tensorrt) |

### Other Containers

| Name | Description | Container Tag | URL |
| :--- | :--- | :--- | :--- |
| _**Flask**_ | A basic Python web server framework | `paperspace/flask` | [DockerHub](https://hub.docker.com/r/paperspace/flask) |

## Also see Custom Deployment Containers

{% page-ref page="custom-deployment-containers.md" %}

