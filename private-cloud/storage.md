# Storage

## About

To make local data accessible within Gradient Private Cloud Jobs, use the `--mount` command to mount one or more directories within the running worker nodes \(containers\).  

This functionality is similar the the [Persistent Storage](../data/managing-data-in-gradient.md#persistent-storage) option \(`/storage`\) which is automatically mounted across all hosted Jobs and Notebooks. 

Syntax: `/path/to/local:path/inside/job-container` for each mount, comma separated.

## Example Use

```text
$ paperspace project show
```

{% hint style="danger" %}
Certain paths are restricted: do not mount `/artifacts`, `/paperspace` or / \(root\) volumes. Home directory for the jobs is `/paperspace`
{% endhint %}

