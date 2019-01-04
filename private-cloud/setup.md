# Setup

## Download

{% hint style="warning" %}
Request access to the Gradient Private Cloud here: [https://paperspace.com/console/clusters](https://www.paperspace.com/console/clusters). Your account will need to be approved access before you can use the Gradient Agent software  to manage your own cluster of GPUs. 

After getting access granted for your account, download the gradient-node binary from the following link. 

Download: [https://s3.amazonaws.com/gradient-node/latest/linux/gradient-node](https://s3.amazonaws.com/gradient-node/latest/linux/gradient-node)

SHA-256 Hash: [https://s3.amazonaws.com/gradient-node/latest/linux/sha256](https://s3.amazonaws.com/gradient-node/latest/linux/sha256)
{% endhint %}

## Installing dependencies

Here is an example set of commands to install the prerequisites on an Ubuntu 16.04 machine:

{% hint style="info" %}
See the Docker and NVIDIA sites for updated installation instructions for more recent versions.

[https://www.nvidia.com/drivers](https://www.nvidia.com/drivers) 

[https://www.docker.com/get-started](https://www.docker.com/get-started)
{% endhint %}

```text
# Updating apt-get cache and installing base certificates package
sudo apt-get update && apt-get install ca-certificates curl software-properties-common

# Adding Docker's apt repository's GPG key. Necessary for trusting Docker's apt repo which is used in next step.
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Adding Docker's apt repo to system.
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Pulling down info from Docker apt repo previously added. Then we're installing Docker.
sudo apt-get update && apt-get install docker-ce=17.12.1~ce-0~ubuntu

# Grabbing GPG key to trust NVIDIA apt repository.
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

# Adding NVIDIA library apt repository to the system.
sudo add-apt-repository "deb https://nvidia.github.io/libnvidia-container/ubuntu16.04/amd64 /"

# Adding NVIDIA container runtime apt repository to system.
sudo add-apt-repository \
"deb https://nvidia.github.io/nvidia-container-runtime/ubuntu16.04/amd64 /"

# Adding NVIDIA Docker apt repository to system.
sudo add-apt-repository "deb https://nvidia.github.io/nvidia-docker/ubuntu16.04/amd64 /"

# Updating apt-get cache and installing necessary NVIDIA packages.
sudo apt-get update && sudo apt-get install nvidia-container-runtime=2.0.0+docker17.12.1-1 nvidia-docker2=2.0.3+docker17.12.1-1

# Installing NFS tools (without the server & client).
sudo apt-get install nfs-common=1:1.2.8-9ubuntu12.1
```

### Running for the first time

```text
# Download latest binary 
wget https://s3.amazonaws.com/gradient-node/latest/linux/gradient-node

# Optional: Download hash to validate authenticity of binary
wget https://s3.amazonaws.com/gradient-node/latest/linux/sha256

# Make binary executable (for all users):
chmod a+x gradient-node

# Optional: Checksum matches binary:
shasum -a 256 gradient-node

# Optional: Display the downloaded sha256 (against previous command):
cat sha256

# Test install:
./gradient-node --version
#show version information
```

