# Overview

Gradient clusters are private clusters that run machine learning workloads. Gradient clusters can be created on Paperspace Cloud as a [managed service](setup/managed-installation.md), directly on Paperspace Core VMs, on any other cloud provider \(AWS, GCP, Azure\), or on your own servers via the [Gradient Installer](setup/self-hosted-clusters/).

Find out more about Gradient's multi-cloud capabilities [here](https://gradient.paperspace.com/clusters).

You can [create a managed Gradient Cluster on Paperspace using the Web UI](https://console.paperspace.com/clusters/create) in a couple of clicks.

## Choosing between our managed service, managed private clusters, and self-hosting Gradient

|  | Managed Service \(multi-tenant\) | Managed Private Clusters | Self-Hosted Clusters |
| :--- | :--- | :--- | :--- |
| **Infrastructure:** | Shared, managed by Paperspace | Private, managed by Paperspace | Private, self-hosted |
| **Setup time:**  | None | Setup time: 10 minutes | Setup time: 20-30 minutes |
| **Features:**  | Notebooks \(including [Free GPUs](../instances/free-instances.md)!\), basic experiments | Notebooks, experiments, deployments, model repo, data management, GradientCI | Notebooks, experiments, deployments, model repo, data management, GradientCI |
| **Target audience:**  | Hobbyists & students | Startups & SMBs running production workloads | Mid-market & enterprise businesses conducting ML at scale |

This section of our documentation covers the private cluster options.  If you are looking to use our managed service, just [create an account](https://console.paperspace.com/signup?gradient=true) to get started right away. 

## Cluster pricing

### Managed 

**Compute, Storage, & Networking**  
The auxiliary compute, storage, and networking cost to run the cluster is $0.13/hr. In addition, instances used to run workloads are charged at the regular rate \(see [instance pricing](../instances/instance-types.md)\) plus a small [compute premium](https://gradient.paperspace.com/private-cluster-utilization-premium).    
  
What's included: Private Clusters require a minimum of one CPU node for cluster orchestration.  The node is a C5 instance \(see [instance pricing](../instances/instance-types.md)\) which costs $0.08/hour.  Additionally, there is a $1/instance/month \(pro-rated, billed per second\) for any nodes in the cluster.  There is also a minimum 500GB storage requirement \(for [persistent storage](../data/storage.md#persistent-storage)\) which is $25/month.  

**Subscription**  
Gradient Private Clusters require a T1 or great [subscription](https://gradient.paperspace.com/pricing).  

### Self-Hosted

**Compute, Storage, & Networking**  
Customers are responsible for their infrastructure costs.  Gradient does not bill for any compute, storage, and networking costs other than the [compute premium](https://gradient.paperspace.com/private-cluster-utilization-premium).  

**Subscription**  
Gradient Private Clusters require a Essentials or great [subscription](https://gradient.paperspace.com/pricing).  

