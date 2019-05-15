# Building a Custom Container

## About

Custom containers feature lets you pull your own image from a container registry eg Docker Hub. This article will help you prepare a custom Docker container to use with Gradient, show you how to bring that Container into Gradient, and create a notebook with your custom container. We recommend using Docker to get the container image from your system to Gradient. 

{% hint style="info" %}
**ProTip!**: Using a Custom Container does not require building one from scratch.  See this article for using one of the many freely available and up-to-date containers hosted on various container registries \(eg [Docker Hub](https://hub.docker.com/), [NGC](https://ngc.nvidia.com/catalog/landing) etc.\).  See this [article](./) for more info.
{% endhint %}

## Preparing a Custom Container

#### 1. To get started, you’ll need:

* An Ubuntu computer with [DockerCE](https://github.com/docker/docker-ce), [NVIDIA-docker](https://github.com/NVIDIA/nvidia-docker), and NVIDIA Drivers installed \(if you don’t have a Linux machine, use a Paperspace Linux VM!\).
* From that machine, you'll need to be logged into your [Docker Hub](https://hub.docker.com/) account  `docker login -u <username> -p <password>`

#### 2. Add a Docker file to a working directory on your system

You can make your own file \(see Requirements below\) or use one like this example: [https://github.com/Paperspace/tensorflow-python](https://github.com/Paperspace/tensorflow-python)

#### 3. In the same directory:

* Run: `docker build -t <name of image>` 

         for the example file above, you would enter: `docker build -t test-container`

* Verify with docker images. It should look something like this:![Screenshot\_2018-08-23\_17.53.29.png](https://support.paperspace.com/hc/article_attachments/360011197753/Screenshot_2018-08-23_17.53.29.png)
* Tag the image so that is can be added to a repo with the image id, your Docker Hub username, and a name for the image :

`docker tag <image id> <dockerhub username>/test-container:latest`

#### 4. Push the image to Docker Hub with your username:

`docker push <username>/test-container:latest`

###  Requirements of Custom Notebooks

* Python
* Jupyter and all of Jupyter dependencies must be installed:

[        http://jupyter.org/install](http://jupyter.org/install)

`conda install -c conda-forge jupyterlab`

If you don't specify a user, your container user will be 'root' 

## Bringing your Custom Container to Paperspace

After you've pushed your custom container to Docker or you found a public container that is already there, it's time to pull it into Paperspace!

[Notebooks Page.](https://www.paperspace.com/console/notebooks/create)  Select Notebooks from your left-hand navigation menu. Click the Custom Containers tab in the Base Containers section. 

* Container Name = Path and tags of image eg ufoym/deepo:all-jupyter-py36
* Username = your Docker Hub username, can be left blank for public images
* Password = your Docker Hub password, can be left blank for public images
* Default Entrypoint = must be Jupyter compatible, defaults to 'jupyter notebook' if left blank
* Container user = optional user, defaults to 'root' if left blank

![](https://support.paperspace.com/hc/article_attachments/360011084754/mceclip1.png)

Follow the rest of the steps to create your Notebook by selecting your machine type, naming your notebook, and clicking Create. 

## Private Containers

If your container is hosted in a password protected repository \(you have set your Docker Image to 'Private'\), you will need to enter your Docker Hub password. Otherwise, leave this field blank. **This is not your Paperspace username and password.**

Privacy settings for a given container might look something like this in Docker Hub: ![Screenshot\_2018-08-24\_15.22.39.png](https://support.paperspace.com/hc/article_attachments/360011177694/Screenshot_2018-08-24_15.22.39.png)

if a Notebook image is private and the password is missing or invalid, the Notebook won't run :\(   

