# Setup

The Gradient installer uses Terraform to provision your cluster; this repo does not provide a standalone program. Think of this repo as a dependency that enables Terraform to create your desired cluster in your target environment and then install Gradient on that cluster. The documentation here and its subsequent sections (targeting AWS, NVIDIA DGX, bare metal, etc.), will lead you step-by-step to create a Terraform configuration from a provided base configuration, and then to use Terraform to create your Gradient cluster. In brief, you'll create a dedicated gradient-cluster folder to contain your Terraform configuration, and then you'll use Terraform itself to install Gradient. You do not need to clone down the `gradient-installer` repo or run anything directly in that repo; rather, the Terraform configuration you will be led to create as follows, will take care of calling out to the code in the `gradient-installer` repo.

Terraform is an open source infrastructure automation tool that manages infrastructure for cloud providers and on-prem solutions. Terraform creates your infrastructure, configures resources, and manages updates of the Gradient software. The purpose of this tool is to automate most of the manual efforts of managing and maintaining distributed systems. 

Using Terraform, Gradient can be installed in different modes: there's an AWS-specific version that creates a Gradient cluster in Amazon's Elastic Kubernetes Service \(EKS\), and a more generic version that can configure bare metal servers or virtual machines in nearly any environment - including NVIDIA's DGX-1 and Google Cloud's Compute Engine.

#### General Prerequisites

* Terraform installed on your computer, or on a cloud instance that has network access to the environment where Gradient will run \(not required for DGX installer mode\)
* Technical familiarity with the cloud provider or private cloud environment where you will install and run Gradient
* SDK or CLI tools installed from your cloud provider, if necessary \(e.g. aws-cli, aws-iam-authenticator\)

#### Pre-installation steps must be completed before visiting the individual installation sections below.

{% page-ref page="pre-installation-steps.md" %}

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

{% page-ref page="install-on-aws.md" %}

{% page-ref page="bare-metal-vms.md" %}

{% page-ref page="install-nvidia-dgx.md" %}
