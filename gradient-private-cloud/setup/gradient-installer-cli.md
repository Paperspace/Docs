# Gradient Installer CLI

Gradient Installer is a CLI to setup and manage Gradient private clusters on AWS, GCP, Azure, NVIDIA DGX-1, and bare metal

Terraform is used under the hood to setup all the infrastructure. Terraform modules can also be used directly to integrate Gradient into an existing Terraform setup.

## Prerequistes

* A Paperspace account with an appropriate billing plan and API key
* An AWS S3 bucket to store Terraform state \[[https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-bucket.html](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-bucket.html)\]

## Installation

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/paperspace/gradient-installer/master/bin/install)"
```

#### 

```text
gradient-installer update
```

## **Usage**

Things to have beforehand:

* AWS credentials to an S3 bucket to store cluster state information
* From [Pre-installation steps](pre-installation-steps.md): artifacts bucket and credentials, SSL certificates or Let's Encrypt Settings
* Domain where Gradient will be accessed
* DNS provider information to register your Gradient domain

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

