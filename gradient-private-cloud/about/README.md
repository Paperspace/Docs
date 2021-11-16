# Overview

Gradient clusters are private clusters that run machine learning workloads. Gradient clusters can be [created](setup/managed-installation.md) on Paperspace Cloud, on any other cloud provider (AWS, GCP, Azure), or on your own servers via the [Gradient Installer](setup/self-hosted-clusters/).

Find out more about Gradient's multi-cloud capabilities [here](https://gradient.paperspace.com/clusters).

You can [create a managed cluster ](https://console.paperspace.com/clusters/create)using the Web UI in a couple of clicks.

## Choosing between our managed service, managed private clusters, and self-hosting Gradient

| **Infrastructure:**   | Shared, managed by Paperspace | Private, managed by Paperspace               | Private, self-hosted                                      |
| --------------------- | ----------------------------- | -------------------------------------------- | --------------------------------------------------------- |
| **Setup time: **      | None                          | Setup time: 10 minutes                       | Setup time: 20-30 minutes                                 |
| **Target audience:**  | Hobbyists & students          | Startups & SMBs running production workloads | Mid-market & enterprise businesses conducting ML at scale |

This section of our documentation covers the private cluster options.  If you are looking to use our managed service, just [create an account](https://console.paperspace.com/signup?gradient=true) to get started right away.&#x20;

## Cluster pricing

### Managed Service

We charge per hour for compute time on _paid_ instances (see our [free tier](../../more/instance-types/free-instances.md)). Optionally, you can upgrade your [subscription](https://gradient.paperspace.com/pricing) to access higher concurrency and additional features.&#x20;

### Managed Private Clusters&#x20;

**Compute, Storage, & Networking**\
****The Kubernetes master node, storage, and networking cost to run the cluster is $0.12/hr. Private Clusters require a minimum of one CPU node for cluster orchestration and clusters include 500GB of storage by default. &#x20;

In addition, instances used to run workloads are charged at the regular rate (see [instance pricing](../../more/instance-types/)) plus a small [compute premium](https://gradient.paperspace.com/private-cluster-utilization-premium). &#x20;

### Self-Hosted

**Compute, Storage, & Networking**\
****Customers are responsible for their infrastructure costs. Gradient does not bill for any compute, storage, and networking costs other than the [compute premium](https://gradient.paperspace.com/private-cluster-utilization-premium). &#x20;

**Subscription**\
Gradient Private Clusters require an Essentials or great [subscription](https://gradient.paperspace.com/pricing). &#x20;
