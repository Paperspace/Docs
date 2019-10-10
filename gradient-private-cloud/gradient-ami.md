---
description: Launch Gradient° on AWS in Seconds
---

# Gradient AMI

As an alternative to setting up Gradient nodes in your cluster manually, Paperspace also publishes an official AMI image that contains the gradient-node software alongside all required dependencies like NVIDIA drivers, CUDA, and nvidia-docker. The AMI is available in the AWS Marketplace and is kept up to date with the latest version of Gradient°. The Paperspace AMI works with all EC2 instances, but GPU acceleration will only work on GPU-enabled instance types.

[Click here to install Gradient on AWS](https://aws.amazon.com/marketplace/pp/B07Q473W7M)

### Technical Details

* AMI Base OS: Ubuntu 16.04 LTS
* Nvidia Drivers: Tesla 410.104
* CUDA Version: 10
* OpenCL drivers included

## Running Gradient° via AMI

Starting a gradient-node from the AMI is simple: select the AMI from the AWS Marketplace when configuring the EC2 instance details. You may either pass in your settings \(like API key, node name, and node cluster\) via user-data \(easy\) or by SSH-ing into the running instance and configuring these options manually \(more difficult\).

#### Configuration Steps in AWS 

1. Choose the AMI from the Marketeplace
2. Select the Instance Type
3. On the Configure Instance step, provide your API key, the node name, node cluster in the Advanced Details dropdown \(using the text option\).  See the [step below](gradient-ami.md#passing-credentials-via-user-data-preferred) for more details.
4. Add your preferred storage 
5. Optional: Add your preferred Tags
6. Set your preferred Security Group.  See the [ports & connectivity](gradient-ami.md#ports-and-connectivity-to-the-gradient-ami-vpc-settings) section below.
7. Launch your new instance
8. On boot, the instance will automatically register with your Gradient account and will be ready to accept Jobs.  See the [usage](usage.md) section for submitting jobs to a Gradient node.

![Once provisioned, the Gradient node will auto register with your account.](../.gitbook/assets/image%20%2829%29.png)

## Passing credentials via user-data \(preferred\)

You can pass credentials into the Gradient° instance at launch time, which enables the node to start automatically and associate itself in your account. You would not have to SSH into the running instance to configure the gradient-node. Below is the text you should copy into the user-data field under "Advanced Details" in Step 3, "Configure Instance Details," when launching an EC2 instance:

![](../.gitbook/assets/image%20%2821%29.png)

```text
#cloud-config

# User defined environmental variables
# Set these to run your gradient-node
    # GRADIENT_NODE_API_KEY       api key, example: GRADIENT_NODE_API_KEY=13x4...48a8
    # GRADIENT_NODE_NAME          name of node in your cluster, example: GRADIENT_NODE_NAME=gradient-node1
    # GRADIENT_NODE_CLUSTER       name of cluster that this node will be assigned to, example: GRADIENT_NODE_CLUSTER=gradient-cluster1

write_files:
- path: /etc/default/gradient-node.env
  content: |
    # EDIT HERE
    GRADIENT_NODE_API_KEY=            
    GRADIENT_NODE_NAME=          
    GRADIENT_NODE_CLUSTER=      
    # DO NOT EDIT BELOW THIS POINT
```

## Customizing your gradient instance

You are free to customize your Gradient° instance as you see fit, by adding dependencies and libraries for example. The name of the Gradient° agent is called `gradient-node`. The agent is run as a systemd service that starts on launch and restarts on errors. Customizing your instance is straightforward:

* SSH into the running instance via `ssh -i your-key.pem ubuntu@public-dns-address`
* Switch to root user via `sudo su`
* Stop the running Gradient° service via `service gradient-node stop`
* Update the instance, install dependencies, etc. May require a reboot. 
* Start the Gradient° service again via `service gradient-node start` 

## Ports & connectivity to the Gradient AMI \(VPC settings\)

The only required ports required for the Gradient AMI to function are 6006 and 8888.  Please ensure TCP traffic can flow on these ports.

