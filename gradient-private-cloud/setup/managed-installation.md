---
description: For creating a private cluster on the Paperspace Cloud.
---

# Managed Private Clusters

## What is a managed private cluster?

Gradient offers a multi-tenant service for running basic ML workloads as well as private clusters that offer more advanced functionality for power users.  Both managed options run on the Paperspace Cloud.  

**How to choose between the multi-tenant service and a private cluster:** If you are doing distributed training, deploying models into production, or need more control over your environment, we recommend creating a private cluster.  

This section covers the managed private cluster option.  If you are looking to use Gradient without a private cluster, just [create an account](https://console.paperspace.com/signup?gradient=true) to get started. If you are looking to run Gradient on your own infrastructure, see the [self-hosted clusters](self-hosted-clusters/) section.  

## Overview

Gradient clusters can be created in just a few clicks in the Web UI as a fully managed service in Paperspace Cloud. Create and run notebooks, experiments, and deployments all in your private cluster from within the Web UI, from the CLI, or using the SDK.

On this page, you'll learn how to create a managed cluster and view your managed clusters from the Web UI.

{% hint style="info" %}
**Note:** Managed clusters require a T1 or greater [subscription](https://gradient.paperspace.com/pricing).
{% endhint %}

{% hint style="warning" %}
**Note:** If you are looking to create a _self-hosted_ Gradient cluster, see the [Gradient Installer CLI](self-hosted-clusters/gradient-installer-cli.md).
{% endhint %}

## Create a managed cluster

### 1. In the Gradient product menu, select **Clusters**

![](https://blog.paperspace.com/content/images/2020/12/Screen-Shot-2020-12-03-at-9.52.27-PM.png)

### 2. Select Create managed cluster

![](https://blog.paperspace.com/content/images/2020/12/Screen-Shot-2020-12-03-at-9.53.19-PM.png)

### 3. Configure your managed cluster

Select the Paperspace Cloud region where your machines will be provisioned, accept the cost \(in this case $26/mo\), and select **Create Cluster**

![](https://blog.paperspace.com/content/images/2020/12/Screen-Shot-2020-12-03-at-9.53.26-PM.png)

### **4. Cluster provisioning**

You should now see that your cluster is provisioning!

This process may take up to 10 minutes of time -- so be prepared to take a quick stretch and use the restroom.

![](https://blog.paperspace.com/content/images/2020/12/Screen-Shot-2020-12-03-at-9.53.37-PM.png)

### 5. Your first managed cluster

When your cluster is successfully provisioned, you will see the new machines now available for your use.

![](https://blog.paperspace.com/content/images/2020/12/Screen-Shot-2020-12-03-at-10.21.13-PM.png)

Once provisioning is completed, the new cluster will appear everywhere in the Web UI that you can select a cluster, including:

* Running notebooks 
* Creating experiments and jobs
* Creating deployments
* Creating a storage provider to connect data
* ... and more!

From the **Clusters** view, you now have access to your cluster and machine details and can Start and Stop your cluster machines manually as needed.

![](../../.gitbook/assets/screen-shot-2020-07-23-at-11.11.52-pm.png)

## View your Managed Clusters

Once you've created any number of managed clusters, you can view them on the same Private Clusters page.

![](../../.gitbook/assets/screen-shot-2020-07-23-at-10.48.52-pm.png)

## Autoscaling Groups

Managed private clusters utilize autoscaling groups so that only the machines you need are active when you need them. Autoscaling groups can be configured by viewing your private cluster.

![](../../.gitbook/assets/screen-shot-2020-09-16-at-8.43.32-pm.png)

Each autoscaling group has the following:

* Machine - this is the machine type that the autoscaling group will manage
* Hot Nodes - standby machines that are on at all times and can process Gradient workloads immediately
* Max Pool Size - Maximum amount of machines that can be created by autoscaling. This value is limited by your account's maximum machine count

Default autoscaling machine types: C5, C7, C10, P4000, P5000, V100

