# Notebook Containers

## Base Containers

When you launch a Notebook, it runs inside a container preloaded with the notebook files and dependencies.  The following is a list of containers that Paperspace maintains:

| Name | Description | URL |
| :--- | :--- | :--- |
| _Fast.ai + PyTorch_ | Paperspace's Fast.ai template is built for getting up and running with the enormously popular [Fast.ai online MOOC called Practical Deep Learning for Coders](http://www.fast.ai/).  | [GitHub](https://github.com/Paperspace/fastai-docker) |
| _TensorFlow \(1.5.0 GPU Py3\)_ | Official docker images for deep learning framework TensorFlow \([http://www.tensorflow.org](http://www.tensorflow.org/)\) | [DockerHub](https://hub.docker.com/r/tensorflow/tensorflow/) |
| _TensorFlow \(1.5.0 CPU Py3\)_ | Official docker images for deep learning framework TensorFlow \([http://www.tensorflow.org](http://www.tensorflow.org/)\) | [DockerHub](https://hub.docker.com/r/tensorflow/tensorflow/) |
| _Deepo \(Python 2.7\)_ | A series of Docker images \(and their generator\) that allows you to quickly set up your deep learning research environment. \([https://hub.docker.com/r/ufoym/deepo](https://hub.docker.com/r/ufoym/deepo)\) | [GitHub](https://github.com/ufoym/deepo) |
| _Deepo \(Python 3.6\)_ | A series of Docker images \(and their generator\) that allows you to quickly set up your deep learning research environment. \([https://hub.docker.com/r/ufoym/deepo](https://hub.docker.com/r/ufoym/deepo)\) | [GitHub](https://github.com/ufoym/deepo) |
| _JupyterLab Data Science Stack_ | Jupyter Notebook Data Science Stack | [DockerHub](https://hub.docker.com/r/jupyter/datascience-notebook/) |
| _JupyterLab Data R Stack_ | Jupyter Notebook R Stack | [DockerHub](https://hub.docker.com/r/jupyter/r-notebook/) |
| _NVIDIA RAPIDS dev ubuntu18.04_ | Suite of open source libraries to execute end-to-end data science and analytics pipelines. Written in Python, and built on Apache Arrow.  |  [Nvidia](https://developer.nvidia.com/rapids) |

## Custom Containers

Custom containers feature lets you pull your own image from Docker Hub. This article will help you prepare a custom Docker container to use with Gradient, show you how to bring that Container into Gradient, and create a notebook with your custom container. We recommend using Docker to get the container image from your system to Gradient. 

Here are the parameters:

* Container Name = Path and tags of image eg ufoym/deepo:all-jupyter-py36
* Username = your Docker Hub username, can be left blank for public images
* Password = your Docker Hub password, can be left blank for public images
* Default Entrypoint = must be Jupyter compatible, defaults to 'jupyter notebook' if left blank
* Container user = optional user, defaults to 'root' if left blank

See a tutorial on using custom containers [here](https://support.paperspace.com/hc/en-us/articles/360008256453-Creating-Using-Custom-Containers-with-Notebooks).

{% hint style="info" %}
This page provides help about pulling containers from various public and private repositories:

[https://support.paperspace.com/hc/en-us/articles/360003415434-Containers-Public-Private](https://support.paperspace.com/hc/en-us/articles/360003415434-Containers-Public-Private) 
{% endhint %}

