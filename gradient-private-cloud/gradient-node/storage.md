# Storage

## About

To make local data accessible within Gradient Private Cloud Jobs, use the `--mounts` command to mount one or more directories within the running worker nodes \(containers\).  

This functionality is similar the the [Persistent Storage](../../data/managing-data-in-gradient/#persistent-storage) option in Paperspace hosted Jobs \(`/storage`\) which is automatically mounted across all Jobs and Notebooks. 

Syntax: `/path/to/local:path/inside/job-container` for each mount, comma separated. 

{% hint style="info" %}
The home directory for all Jobs is `/paperspace`. 
{% endhint %}

{% hint style="danger" %}
Certain paths are restricted: do not mount `/artifacts`, `/paperspace` or / \(root\) volumes.  
{% endhint %}

## Example Use

```text
$ ./gradient-node --mounts /local/folder:/paperspace/data ...
```

