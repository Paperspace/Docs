---
description: Launch gradient on AWS in seconds
---

# Gradient AMI

As an alternative to setting up gradient nodes in your cluster manually, Paperspace also publishes an official AMI image that contains the gradient-node software alongside all required dependencies like NVIDIA drivers, CUDA, and nvidia-docker. The AMI is available in the AWS Marketplace and is kept up to date with the latest version of gradient. The Paperpsace AMI works with all EC2 instances but GPU acceleration will only work on GPU-enabled instance types. 

### Technical Details

* AMI Base OS: Ubuntu 16.04 LTS
* Nvidia Drivers: Tesla 410.104
* CUDA Version: 10
* OpenCL drivers included

### Running gradient via AMI

Starting a gradient-node from the AMI is simple: simply select the AMI from the AWS Marketplace when configuring the EC2 instance details. You may either pass in your settings \(like API key, node name, and node cluster\) via user-data \(easy\) or by ssh-ing into the running instance and configuring these options manually \(more difficult\). 

### Passing credentials via user-data \(preferred\)

You can pass credentials into the gradient instance at launch type, which enables the node to start automatically and associate itself in your account. You would not have to ssh into the running instance to configure the gradient-node. Below is the text you should copy into user-data field under "Advanced Details" in Step 3 Configure Instance Details when launching an EC2 instance: 

![](../.gitbook/assets/image%20%285%29.png)

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

### Customizing your gradient instance

You are free to customize your gradient instance as you see fit, by adding dependencies and libraries for example. The name of the gradient agent is called `gradient-node`.  The agent is run as a systemd service that starts on launch and restarts on errors. Customizing your instance is straightforward:

* ssh into the running instance via `ssh -i your-key.pem ubuntu@public-dns-address`
* Switch to root user via `sudo su`
* Stop the running gradient service via `service gradient-node stop`
* Update the instance, install dependencies, etc. May require a reboot. 
* Start the gradient service again via `service gradient-node start` 

