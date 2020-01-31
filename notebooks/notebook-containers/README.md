# Notebook Containers

## Base Containers

When you launch a Notebook, it runs inside a container preloaded with the notebook files and dependencies.  The following is a list of containers that Paperspace maintains:

### Popular Containers

| Name | Description | Container Tag | URL |
| :--- | :--- | :--- | :--- |
| _**Fast.ai**_                | Paperspace's Fast.ai template is built for getting up and running with the enormously popular [Fast.ai online MOOC](http://www.fast.ai/).  | `paperspace/fastai:1.0-CUDA9.2-base-3.0-v1.0.6` | [GitHub](https://github.com/Paperspace/fastai-docker) |
| _**All-in-one**_ | All ML/DL frameworks in a single template with CUDA/cuDNN and other libraries. Python 36. | `ufoym/deepo:all-py36-jupyter` | [GitHub](https://github.com/ufoym/deepo) |
| _**TensorFlow 2.0**_ | Preview of TensorFlow 2.0 with GPU support. Python 36. | `tensorflow/tensorflow:2.0.0a0-gpu-py3-jupyter` | \*\*\*\*[DockerHub](https://hub.docker.com/r/tensorflow/tensorflow) |
| _**NVIDIA RAPIDS**_ | NVIDIA's open source libraries to execute end-to-end data science and analytics pipelines. v0.8. | `cuda10.0-devel-ubuntu18.04` |  [NVIDIA](https://hub.docker.com/r/rapidsai/rapidsai/tags) |
| _**PyTorch**_ | Latest PyTorch release \(1.2\) with GPU support. Python 36. | `paperspace/dl-containers:pytorch-py36-cu100-jupyter` | [DockerHub](https://hub.docker.com/r/pytorch/pytorch) |
| _**TensorFlow**_ | Latest stable release \(1.14.0\) with GPU support. Python 36. | `paperspace/dl-containers:tensorflow1140-py36-cu100-cdnn7-jupyter` | [DockerHub](https://hub.docker.com/r/tensorflow/tensorflow) |

### Other Containers

| Name | Description | Container Tag | URL |
| :--- | :--- | :--- | :--- |
| _**TensorFlow \(1.5.0 GPU Py3\)**_ | Official docker images for deep learning framework TensorFlow \([http://www.tensorflow.org](http://www.tensorflow.org/)\) | `tensorflow/tensorflow:1.5.0-gpu-py3` | [DockerHub](https://hub.docker.com/r/tensorflow/tensorflow/) |
| _**TensorFlow \(1.5.0 CPU Py3\)**_ | Official docker images for deep learning framework TensorFlow \([http://www.tensorflow.org](http://www.tensorflow.org/)\) | `tensorflow/tensorflow:1.5.0-py3` | [DockerHub](https://hub.docker.com/r/tensorflow/tensorflow/) |
| _**Deepo \(Python 2.7\)**_ | A series of Docker images \(and their generator\) that allows you to quickly set up your deep learning research environment. \([https://hub.docker.com/r/ufoym/deepo](https://hub.docker.com/r/ufoym/deepo)\) | `ufoym/deepo:all-py27-jupyter` | [GitHub](https://github.com/ufoym/deepo) |
| _**JupyterLab Data Science Stack**_ | Jupyter Notebook Data Science Stack | `jupyter/datascience-notebook` | [DockerHub](https://hub.docker.com/r/jupyter/datascience-notebook/) |
| _**JupyterLab Data R Stack**_ | Jupyter Notebook R Stack | `jupyter/r-notebook` | [DockerHub](https://hub.docker.com/r/jupyter/r-notebook/) |

## Custom Containers

Custom containers feature lets you pull your own image from a container registry such as Docker Hub. This article will help you prepare a custom Docker container to use with Gradient, show you how to bring that Container into Gradient, and create a notebook with your custom container. We recommend using Docker to get the container image from your system to Gradient. 

#### Required field:

* Container Name = Path and tags of image eg `ufoym/deepo:all-jupyter-py36`

![](../../.gitbook/assets/image%20%2879%29.png)

#### Optional fields:

* Username = your Docker Hub username, can be left blank for public images
* Password = your Docker Hub password, can be left blank for public images
* Default Entrypoint = must be Jupyter compatible, defaults to 'jupyter notebook' if left blank
* Container user = optional user, defaults to 'root' if left blank

See a tutorial on using custom containers [here](building-a-custom-container.md).

