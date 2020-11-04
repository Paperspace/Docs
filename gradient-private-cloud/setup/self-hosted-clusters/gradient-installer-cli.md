# Gradient Installer CLI

Gradient Installer is a CLI to set up and manage Gradient private clusters on AWS, GCP, Azure, NVIDIA DGX, and bare metal.

Terraform is used under the hood to setup all the infrastructure. Terraform modules can also be used directly to integrate Gradient into an existing Terraform setup.

## Prerequisites

* Paperspace account with an appropriate billing plan and API key
* [AWS S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-bucket.html) to store Terraform state

## Installation

To install the Gradient Installer CLI, run the following command:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/paperspace/gradient-installer/master/bin/install)"
```

#### 

```text
gradient-installer update
```

## **Profiles**

Gradient Installer CLI support multiple profiles. To setup the CLI with a different profile run:

```text
export PAPERSPACE_PROFILE=favorite-team
gradient-installer setup
```

## **Usage**

### Additional Prerequisites

* AWS credentials to an S3 bucket to store cluster state information
* From [Pre-installation steps](pre-installation-steps.md): artifacts bucket and credentials, SSL certificates or Let's Encrypt Settings
* Domain where Gradient will be accessed
* DNS provider information to register your Gradient domain
* (Optional): Service account credentials for a container registry such as Docker Hub. Notebook snapshots and container builds are pushed to this registry.

### Setting up a new cluster

```text
gradient-installer clusters up
```

This will prompt you for information to register and create your private cluster. 

### Setting up or upgrading an existing cluster

```text
gradient-installer clusters up CLUSTER_HANDLE
```

### Uninstalling a cluster

```text
gradient-installer clusters down CLUSTER_HANDLE
```

