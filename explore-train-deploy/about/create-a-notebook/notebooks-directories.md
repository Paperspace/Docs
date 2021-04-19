# Notebook Directories

{% hint style="info" %}
**Note**: This document covers how storage works in Notebook instances only. See our [Data](../../../data/data-overview/) section for a comprehensive overview of managing data in Gradient.
{% endhint %}

## Types of Notebook Storage

### 1. Overlay

This is the root filesystem of the container \(not the workspace nor persistent storage which are covered below\). This space becomes baked into the container image upon teardown. Meaning, if you write say 2GB of data to root by installing various packages \(or storing data in this location\) -- this will now be part of the base root on next run and the quota limit resets. **This directory is capped at 8GB.**

### 2. Workspace

This is a **local** docker volume mounted onto `/notebooks` and currently has a hard limit of 250GB. This directory and the entirety of its contents are stored persistently on a cluster. Some files are uploaded to be visible in the console or to be accessible in forks by default this is only `.ipynb` files. See [notebook include files](https://github.com/Paperspace/Docs/tree/9f5869e1aef4b75067075530e65c9764279782bf/notebook-include.md) for full details.

### 3. /storage or /notebooks/storage

This is persistent storage which is an NFS mount of a volume on a storage server. This quota/size is determined by the team subscription so can range from 5GB up to 1TB. [Contact sales](https://info.paperspace.com/contact-sales) if you need to increase this limit beyond what is available with the default subscription plans\).

