# Notebook Containers

{% hint style="success" %}
Check out the [ML Showcase](https://ml-showcase.paperspace.com/) for a list of projects you can fork into your account.
{% endhint %}

## Base Containers

When you launch a Notebook, it runs inside a container preloaded with the notebook files and dependencies.  The following is a list of containers that Paperspace maintains:

### Popular Containers

| Name | Description | Container Tag | URL |
| :--- | :--- | :--- | :--- |
| _**Fast.ai**_                | Paperspace's Fast.ai template is built for getting up and running with the enormously popular [Fast.ai online MOOC](http://www.fast.ai/).  | `paperspace/fastai:2.0-CUDA9.2-fastbook-v0.1.0` | [GitHub](https://github.com/Paperspace/fastai-docker) |
| _**TensorFlow 2.4.1**_ | TensorFlow 2 with GPU support.  | `tensorflow/tensorflow:2.4.1-gpu-jupyter` | \*\*\*\*[DockerHub](https://hub.docker.com/r/tensorflow/tensorflow) |
| _**NVIDIA RAPIDS**_ | NVIDIA's library to execute end-to-end data science and analytics pipelines. | `nvcr.io/nvidia/rapidsai/rapidsai:0.18-cuda11.0-base-centos7` |  [NVIDIA](https://hub.docker.com/r/rapidsai/rapidsai/tags) |
| _**PyTorch**_ | Latest PyTorch release \(1.8\) with GPU support.  | `nvcr.io/nvidia/pytorch:21.02-py3` | [DockerHub](https://hub.docker.com/r/pytorch/pytorch) |
| _**Hugging Face Transformers**_ | A state-of-the-art NLP library from Hugging Face | `paperspace/transformers-gpu:0.4.0` | [DockerHub](https://hub.docker.com/r/paperspace/transformers-gpu) |

### Other Containers

| Name | Description | Container Tag | URL |
| :--- | :--- | :--- | :--- |
| _**TensorFlow \(1.14 GPU\)**_ | Official docker images for deep learning framework TensorFlow | `paperspace/dl-containers:tensorflow1140-py36-cu100-cdnn7-jupyter` | [DockerHub](https://hub.docker.com/r/tensorflow/tensorflow/) |
| _**Analytics Vidhya CV**_ | Analytics Vidhya conatiner  | `jalfaizy/cv_docker:latest` | [GitHub](https://github.com/ufoym/deepo) |
| _**JupyterLab Data Science Stack**_ | Jupyter Notebook Data Science Stack | `jupyter/datascience-notebook` | [DockerHub](https://hub.docker.com/r/jupyter/datascience-notebook/) |
| _**JupyterLab Data R Stack**_ | Jupyter Notebook R Stack | `jupyter/r-notebook` | [DockerHub](https://hub.docker.com/r/jupyter/r-notebook/) |

## Custom Containers

Custom containers feature lets you pull your own image from a container registry such as Docker Hub. This article will help you prepare a custom Docker container to use with Gradient, show you how to bring that Container into Gradient, and create a notebook with your custom container. We recommend using Docker to get the container image from your system to Gradient. 

#### Required field:

* Container Name = Path and tags of image eg `ufoym/deepo:all-jupyter-py36`

![](../../../.gitbook/assets/image%20%288%29.png)

#### Optional fields:

* Registry Username = your private container registry username, can be left blank for public images
* Registry Password = your private container registry password, can be left blank for public images
* Command = must be Jupyter compatible, defaults to `jupyter notebook --allow-root --ip=0.0.0.0` if left blank
* Container user = optional user, defaults to 'root' if left blank

