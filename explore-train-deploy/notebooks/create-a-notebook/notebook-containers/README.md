# Notebook containers

{% hint style="success" %}
Check out the [ML Showcase](https://ml-showcase.paperspace.com) for a list of projects you can fork into your account.
{% endhint %}

## Base Containers

When you launch a Notebook, it runs inside a container preloaded with the notebook files and dependencies. The following is a list of containers that Paperspace maintains:

### Popular Containers

### Other Containers

| Name                                | Description                                     | Container Tag                                                      | URL                                                                 |
| ----------------------------------- | ----------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------- |
| _**TensorFlow (1.14 GPU)**_         | Official docker images for TensorFlow version 1 | `paperspace/dl-containers:tensorflow1140-py36-cu100-cdnn7-jupyter` | [DockerHub](https://hub.docker.com/r/tensorflow/tensorflow/)        |
| _**Analytics Vidhya CV**_           | Analytics Vidhya container                      | `jalfaizy/cv_docker:latest`                                        | [GitHub](https://github.com/ufoym/deepo)                            |
| _**JupyterLab Data Science Stack**_ | Jupyter Notebook Data Science Stack             | `jupyter/datascience-notebook`                                     | [DockerHub](https://hub.docker.com/r/jupyter/datascience-notebook/) |
| _**JupyterLab Data R Stack**_       | Jupyter Notebook R Stack                        | `jupyter/r-notebook`                                               | [DockerHub](https://hub.docker.com/r/jupyter/r-notebook/)           |

## Custom Containers

The custom containers feature lets you pull your own image from a container registry such as Docker Hub. This section will help you prepare a custom Docker container to use with Gradient, show you how to bring that Container into Gradient, and create a notebook with your custom container. We recommend using Docker to get the container image from your system to Gradient. You must run `jupyter` on port `8888` and allow connections from ip address `0.0.0.0`.

To support our notebook IDE, if your command is `jupyter notebook` you must also include the following flags

`--no-browser --NotebookApp.trust_xheaders=True --NotebookApp.disable_check_xsrf=False --NotebookApp.allow_remote_access=True --NotebookApp.allow_origin='*'` &#x20;

If your command is `jupyter lab` use these instead

`--no-browser --LabApp.trust_xheaders=True --LabApp.disable_check_xsrf=False --LabApp.allow_remote_access=True --LabApp.allow_origin='*'`

#### Required field:

* Container Name = Path and tags of image, e.g., `ufoym/deepo:all-jupyter-py36`

![](<../../../../.gitbook/assets/image (8).png>)

#### Optional fields:

* Registry Username = your private container registry username. Can be left blank for public images.
* Registry Password = your private container registry password. Can be left blank for public images. You can use secrets in this fields using the substitution syntax `secret:`
* Command = must be Jupyter compatible; defaults to `jupyter notebook --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.trust_xheaders=True --NotebookApp.disable_check_xsrf=False --NotebookApp.allow_remote_access=True --NotebookApp.allow_origin='*'` if left blank
* Container user = optional user; defaults to 'root' if left blank
