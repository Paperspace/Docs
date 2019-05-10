# Notebook Containers

## Base Containers

When you launch a Notebook, it runs inside a container preloaded with the notebook files and dependencies.  See the list of containers that Paperspace maintains [here](https://support.paperspace.com/hc/en-us/articles/360001597074-Base-Containers).

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

