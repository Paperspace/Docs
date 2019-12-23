# Managing Data in Gradient

## Persistent Storage

[Persistent Storage](storage.md#persistent-storage) is accessible across Paperspace VM instances and Gradient Experiments, Jobs, and Notebooks.  Uploading and downloading data is possible from any of these endpoints. 

### Uploading

#### From A Notebook

When opening your notebook you will see a `/storage` folder. Clicking on the folder will take you to Persistent Storage where you can upload your data.  If there are a large amount of files, it's advisable to zip them up first. 

![](../.gitbook/assets/image%20%2831%29.png)

#### From a Virtual Machine \(VM\)

To upload data into `/storage` , you can either SCP data from a local laptop/desktop to a Paperspace VM instance or use the upload functionality from within a Gradient Jupyter Notebook.  See a tutorial [here](https://support.paperspace.com/hc/en-us/articles/360005984973-Access-Persistent-Storage-from-a-VM-and-Gradient-).

### Downloading

Downloading data to `/storage` is as simple as using `curl` or `wget` from a Gradient Job or Notebook or Paperspace VM instance.  Alternatively, you can use a browser from within a Paperspace VM instance to download files.

## Artifacts

### Get

Get the artifacts files for the job with the given id. The name of a particular file, or directory can be specified, and can include a wildcard character at the end, e.g., "myfiles"\*. If no specifc file or directory is specified all artifact files will be retrieved.

#### Example Use

```text
$ paperspace jobs artifactsGet --jobId "j123abc"
```

#### **Properties**

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `jobId` | string |  | Id of the job to get artifacts for |
| `files` | string | &lt;optional&gt; | Optional; if getting only certain files, a wildcard pattern to match against, e.g., "myfiles\*". Note: if you include a wildcard you must double-quote the files argument. |
| `dest` | string | &lt;optional&gt; | Optional; an existing directory to copy the artifacts files to. |
| `json` | boolean | &lt;optional&gt; | Optional; return JSON object instead of writing to standard out. '--json' with no value is equivalent to true. |

### List

List job artifact files for the specified job.

#### Example Use

```text
$ paperspace jobs artifactsList --jobId "j123abc" --size true
```

#### Properties

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `jobId` | string |  | Id of the job to list artifacts for |
| `files` | string | &lt;optional&gt; | Optional; wildcard expression of file\(s\) to list, e.g., "myfiles\*". Note: if you include a wildcard you must double-quote the files argument. |
| `size` | boolean | &lt;optional&gt; | Optional; include file size in bytes. '--size' with no value is equivalent to true. |
| `links` | boolean | &lt;optional&gt; | Optional; include https links to artifacts. Note: links are only valid for 8 hours. '--links' with no value is equivalent to true. |
| `json` | boolean | &lt;optional&gt; | Optional; return JSON object instead of writing to standard out. '--json' with no value is equivalent to true. |

### Destroy

Destroy artifact files of the job with the given id. The name of a particular file, or directory can be specified, and can include a wildcard character at the end, e.g., "myfiles\*". If no specifc file or directory is specified all artifact files will be destroyed.

#### Example Use

```text
$ paperspace jobs artifactsDestroy --jobId "j123abc" --files "myfiles*"
```

#### **Properties**

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `jobId` | string |  | The id of the job to destroy artifacts for |
| `files` | string | &lt;optional&gt; | Optional; if destroying only certain files, a wildcard pattern to match against, e.g., "myfiles\*". Note: if you include a wildcard you must double-quote the files argument. |

