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
# Updating apt-get cache and installing base certificates package.
sudo apt-get update && apt-get install ca-certificates curl software-properties-common

# Adding Docker's apt repository's GPG key. Necessary for trusting Docker's apt repo.
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Adding Docker's apt repo to system.
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Pulling down info from Docker apt repo previously added. Then we're installing Docker.
sudo apt-get update && apt-get install docker-ce=18.06.0~ce~3-0~ubuntu

# Grabbing GPG key to trust NVIDIA apt repo.
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

# Adding NVIDIA library apt repo to the system.
sudo add-apt-repository "deb https://nvidia.github.io/libnvidia-container/ubuntu16.04/amd64 /"

# Adding NVIDIA container runtime apt repo to system.
sudo add-apt-repository \
"deb https://nvidia.github.io/nvidia-container-runtime/ubuntu16.04/amd64 /"

# Adding NVIDIA Docker apt repo to system.
sudo add-apt-repository "deb https://nvidia.github.io/nvidia-docker/ubuntu16.04/amd64 /"

# Updating apt-get cache and installing necessary NVIDIA packages.
sudo apt-get update && sudo apt-get install nvidia-container-runtime=2.0.0+docker18.06.0-1 nvidia-docker2=2.0.3+docker18.06.0-1

# Installing NFS tools.
sudo apt-get install nfs-common=1:1.2.8-9ubuntu12.1

# (Optional) Install kaniko container image to run gradient jobs from Dockerfiles
docker images | grep -q gcr.io/kaniko-project/executor || docker pull gcr.io/kaniko-project/executor:latest
```

### Running for the first time

```text
# Download the latest binary.
wget https://s3.amazonaws.com/gradient-node/latest/linux/gradient-node

# Optional: Download the matching hash to validate authenticity of binary.
wget https://s3.amazonaws.com/gradient-node/latest/linux/sha256

# Make binary executable (for all users).
chmod a+x gradient-node

# Optional: Verify checksum matches binary.
shasum -a 256 gradient-node

# Optional: Display the downloaded sha256 (against previous command).
cat sha256

# Test install (show version info).
./gradient-node --version
```

## Getting Help with commands

```text
./gradient-node --help
```

## Updating

To update, simply remove the binary and download the latest version. 

```text
rm -f gradient-node
wget https://s3.amazonaws.com/gradient-node/latest/linux/gradient-node
chmod a+x gradient-node
```

