# Notebooks Directories

{% hint style="info" %}
**Note**: This document covers how storage works in Notebook instances only.  See our [Data](../../data/storage.md) section for a comprehensive overview of managing data in Gradient.
{% endhint %}

## Types of Notebook Storage 

### 1. Overlay

This is the root filesystem of the container \(not the workspace nor persistent storage which are covered below\). This space becomes baked into the container image upon teardown. Meaning, if you write say 2GB of data to root by installing various packages \(or storing data in this location\) -- this will now be part of the base root on next run and the quota limit resets. **This directory is capped at 8GB.**

### 2. Workspace 

This is a **local** docker volume mounted onto `/notebooks` and currently has a hard limit of 25GB. This data is uploaded to S3 and downloaded anew on each run. Which means, it is counted against this quota in summation.

### 3. /storage or /noteboks/storage

This is persistent storage which is an NFS mount of a volume on a storage server. This quota/size is determined by the team subscription so can range from 5GB up to 1TB. [Contact sales](https://info.paperspace.com/contact-sales) if you need to increase this limit beyond what is available with the default subscription plans\).

