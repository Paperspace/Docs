# Managing Data in Gradient

[Persistent Storage](untitled.md#persistent-storage) is accessible across Paperspace VM instances and Gradient Jobs and Notebooks.  Uploading and downloading data is possible from any of these endpoints. 

Once you have set up either a Gradient Notebook or a Job you will have access to Persistent Storage in `/storage`.

### Uploading

To upload data into `/storage` , you can either SCP data from a local laptop/desktop to a Paperspace VM instance or use the upload functionality from within a Gradient Jupyter Notebook.  

### Downloading

Downloading data to /storage is as simple as using `curl` or `wget` from a Gradient Job or Notebook or Paperspace VM instance.  Alternatively, you can use a browser from within a Paperspace VM instance to download files.

See a full tutorial [here](https://support.paperspace.com/hc/en-us/articles/360005984973-Access-Persistent-Storage-from-a-VM-and-Gradient-).

