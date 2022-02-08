# Custom Containers

## Building a custom container

The Custom Containers feature lets you pull your own image from a container registry e.g., Docker Hub. This section will help you prepare a custom Docker container and show you how to bring that Container into Gradient by creating either a Notebook, Workflow, or Deployment with your custom container.&#x20;

{% hint style="info" %}
**ProTip!** Using a Custom Container does not require building one from scratch.  See this [article](../../explore-train-deploy/notebooks/create-a-notebook/notebook-containers/) to access many freely available and up-to-date containers hosted on various container registries (e.g., [Docker Hub](https://hub.docker.com), [NGC](https://ngc.nvidia.com/catalog/landing) etc.).
{% endhint %}

## Build a Custom Container Locally

### Getting started

A computer with [DockerCE](https://github.com/docker/docker-ce), [NVIDIA-docker](https://github.com/NVIDIA/nvidia-docker), and NVIDIA Drivers installed (if you don’t have a Linux machine, use a [Paperspace Linux VM](https://www.paperspace.com/pricing)!).

From that machine, you'll need to be logged into your [Docker Hub](https://hub.docker.com) account in the terminal. \
`docker login -u <username> -p <password>`

You can make your own Docker file from scratch (see "Requirements for for Custom Notebooks" below) or use another as a basis, such as this [example](https://github.com/gradient-ai/tensorflow-python/blob/master/Dockerfile). For now, let's follow along this provided sample.

### Adding a Docker file to a working directory on your system

First, clone the repo, and navigate to the corresponding directory in your terminal.&#x20;

Open the Docker file into your IDE of choice, and make edits as necessary. The provided Docker file sample above pulls from DockerHub a Paperspace-made TensorFlow image designed to run TensorFlow 2.0 for GPUs on Gradient. You can do so with the `FROM` instruction.

Example: `FROM docker.io/tensorflow/tensorflow:latest-gpu-jupyter`

Once your Dockerfile is written, save it, and navigate back to the terminal.

### Building the Docker image

Now that the Docker file is written, we can build the image by running:

&#x20;`docker build -t <Name of image>`&#x20;

For the example file above, you could enter:&#x20;

`docker build test-container`

Once you have created the image, you need to tag it so that it can be added to Docker Hub. Tag the image using the image id, your Docker Hub username, and a name for the image in the following format:

`docker tag <Image id> <Docker username>/test-container:<Tag>`

### Pushing to Docker Hub

Now that we have created and tagged out container, we can push it to Docker Hub for use with our Gradient resources. Use the following `docker push` command to do so:&#x20;

`docker push <Docker username>/test-container:<tag>`

### &#x20;Requirements to use with Custom Notebooks&#x20;

The following should be included in your Docker file to ensure the Notebook will set up and run properly.&#x20;

* Python: \
  `RUN apt-get update && apt-get install -y` `python3 python3-pip`
* Jupyter and all of Jupyter's dependencies: \
  `RUN pip install jupyterlab`\
  ``(For more details, see [http://jupyter.org/install](http://jupyter.org/install))
* If you don't specify a user, your container user will be 'root'

## Bringing your Custom Container to Gradient

After you've pushed your custom container to Docker Hub, NGC, etc., or you found a public container that is already there, it's time to pull it into Gradient!

### Notebooks &#x20;

Click the advanced options toggle on the notebook create a notebook page. Follow the rest of the steps [here](../../explore-train-deploy/notebooks/create-a-notebook/notebook-containers/#custom-containers) to create your Notebook by selecting your machine type, naming your notebook, and clicking Create.&#x20;

### Workflows

Just specify the path of the container e.g., `paperspace/gradient-sdk` from within a Workflow step using `image`. Learn more [here](../../explore-train-deploy/workflows/).

### Deployments

On the Choose Container step, navigate to the custom container tab and fill out the form. Note: A username and password must be provided for private Docker images. &#x20;
