# Setup

## Download

{% hint style="warning" %}
Request access to the downloadable binary here: [https://paperspace.com/console/clusters](https://dev.paperspace.io/console/clusters) 
{% endhint %}

## Installation

Here is an example set of commands to install the prerequisites on an Ubuntu 16.04 machine:

{% hint style="info" %}
See the Docker and NVIDIA sites for updated installation instructions for more recent versions.
{% endhint %}

```text
sudo apt-get update && apt-get install ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"


sudo apt-get update && apt-get install docker-ce=17.12.1~ce-0~ubuntu

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

sudo add-apt-repository "deb https://nvidia.github.io/libnvidia-container/ubuntu16.04/amd64 /"
sudo add-apt-repository \
"deb https://nvidia.github.io/nvidia-container-runtime/ubuntu16.04/amd64 /"
sudo add-apt-repository "deb https://nvidia.github.io/nvidia-docker/ubuntu16.04/amd64 /"

sudo apt-get update && sudo apt-get install nvidia-container-runtime=2.0.0+docker17.12.1-1 nvidia-docker2=2.0.3+docker17.12.1-1

sudo apt-get install nfs-common=1:1.2.8-9ubuntu12.1
```



