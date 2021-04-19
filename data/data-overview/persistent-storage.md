# Persistent Storage

## Persistent Storage

[Persistent Storage](./#persistent-storage) is accessible across Paperspace VM instances and Gradient Experiments, Jobs, and Notebooks.  Uploading and downloading data is possible from any of these endpoints. 

### Uploading

#### From A Notebook

{% embed url="https://youtu.be/FqMClvLnpRQ" %}

When opening your notebook you will see a `/storage` folder. Clicking on the folder will take you to Persistent Storage where you can upload your data.  If there are a large amount of files, it's advisable to zip them up first. 

![](../../.gitbook/assets/image%20%2864%29.png)

#### From a Virtual Machine \(VM\)

To upload data into `/storage` , you can either SCP data from a local laptop/desktop to a Paperspace VM instance or use the upload functionality from within a Gradient Jupyter Notebook.  See a tutorial [here](https://docs.paperspace.com/gradient/data/managing-data-in-gradient/managing-persistent-storage-with-vms).

### Downloading

Downloading data to `/storage` is as simple as using `curl` or `wget` from a Gradient Job or Notebook or Paperspace VM instance.  Alternatively, you can use a browser from within a Paperspace VM instance to download files.

