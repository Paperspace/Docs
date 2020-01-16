# Deployment Containers

## Base Containers

When you launch a Notebook, it runs inside a container preloaded with the notebook files and dependencies.  The following is a list of containers that Paperspace maintains:

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

