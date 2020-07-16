# Using Notebooks

{% tabs %}
{% tab title="Web UI" %}
## Create a Notebook

{% embed url="https://youtu.be/37QZBEtWyp0" %}

### Choose your Base Container

Notebooks can be created by clicking _Create Notebook_ button on the Notebooks tab.  There are three types of base containers:

#### Popular Containers \(Basic\)

These are the templates that are most popular on Gradient.  They include the most common ML frameworks and libraries.  [Click here](../notebook-containers/) to discover which Notebook Base Container will best suit your use case, then choose it from the options below:

![](../../.gitbook/assets/image%20%2868%29.png)

#### All Containers \(Basic\)

These are additional templates that are made available in Gradient as a 1-click option.  [Click here](../notebook-containers/) to discover which Notebook Base Container will best suit your use case, then choose it from the options below:

![](../../.gitbook/assets/image%20%284%29.png)

#### Custom Containers \(Advanced\)

If you need to import an existing container, visit the Custom Containers section. Learn more [here](../notebook-containers/).

### 

![](../../.gitbook/assets/image%20%2860%29%20%281%29.png)

### Choose the instance type

This is [instance type](../../instances/instance-types.md) that your notebook will run on. Our hardware is configured to work with the tools and packages in each of the provided containers.

![](../../.gitbook/assets/image%20%2845%29.png)

### Optional Settings:

#### Name your Notebook

Provide a friendly name for your Notebook in the text field

#### Auto-shutdown

If you have a [Gradient subscription](https://gradient.paperspace.com/pricing), you will have the ability to set a custom auto-shutdown interval. 

If you do not have a Gradient subscription, your notebook will default to an auto-shutdown interval of 12 hours, to help avoid unexpected runtime charges. Once created, you can stop, start, fork, and swap out the instance type anytime. 

**Workspaces**

Additionally, you have the option to select a remote Github repository to serve as [workspace storage](https://docs.paperspace.com/gradient/data/storage#workspace-storage) for your Notebook.  If the repository is private, you need to provide access credentials \(aka username and a password or api-Key.  Note: an api-Key is required if two-factor-authentication is enabled on your account\).  Also, you can provide an optional Github ref \(tag, branch, or commit\) that points to a specific version of the repository.

### Click Create

That's it! Your Notebook will start once it has been created 🚀

Once created, your Notebook will automatically start.  Just click _Open_ and your Notebook will appear in a new browser tab.

## Start a Notebook

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LHZRFUkajubOAmgu6Rd%2F-LeX9E8cIJ_UtEyU8jjp%2F-LeXCI4qsQKD3diF1A78%2Fimage.png?alt=media&token=b6f49118-162d-4b0b-b638-07e767605410)

When you click _Start_, a window will appear that presents a few options such as the name, the instance type, and the Auto-Shutdown interval.

## Stop a Notebook

Click the _Stop_ button to stop your Notebook from running. When your Notebook is stopped, the billing session will end. You'll see how long your Running Time was for the latest session.

## Delete a Notebook

Click Delete to remove your Notebook. Careful - this will permanently delete your Notebook!

{% hint style="info" %}
You can only delete a notebook once it has stopped running.
{% endhint %}

![](../../.gitbook/assets/delete-notebook.png)

## Rename a Notebook

You can rename any Notebook, whether it is running or stopped, in order to help organize your work. Simply click on the notebook name in the list and it will become an editable text field; press the enter key when you are done to save it:

![](../../.gitbook/assets/rename_notebook.png)
{% endtab %}

{% tab title="CLI" %}
### Syntax

```bash
gradient notebooks create [command] [options...]
```

### Notebook Parameters Basics

* Machine Type: Such as `--P100` or `--C7` or `--TPU`
* Container: Such as `--tensorflow/tensorflow:1.5.1-gpu`

### Example Use

```bash
Usage: gradient notebooks create \
    --name "my job" \
    --container "http://dockerhub.com/mycontainer" \
    --machineType "P5000" \
    --command "/paperspace/run.sh"
    --projectId "someProjectID"
```

## Notebook Parameters Complete List

| Argument | Description |
| :--- | :--- |
| `name` | Notebook name |
| `projectId` | Project ID |
| `machineType` \[Required\] | An optional machine type to run the job on: either 'GPU+', 'P4000', 'P5000', 'P6000', 'V100', 'K80', 'P100', or 'TPU'. |
| `container` \[Required\] | A reference to a docker image in a public or private docker registry. Docker image repository references must be in lowercase and may include a tag and a hostname prefix followed by a slash; if committed the hostname defaults to that of the public Docker Hub registry. An example docker image reference: `docker.io/mynamespace/myimage:mytag`. A container name may be mixed case.  |
| `containerUser` | Container user |
| `command` | Command \(executed as `/bin/sh -c 'YOUR COMMAND'`\) |
| `clusterId` | ID of the cluster to run the notebook. |
| `registryUsername` | Registry username |
| `registryPassword` | Registry password |
| `shutdownTimeout` | Shutdown timeout in hours |
| `isPreemptible` | Use a preemptible instance type |
| `tag` |  One or multiple tags that you want to add to the notebook |
| `workspace` | Coming soon |
| `apiKey` | API key to use this time only |
{% endtab %}
{% endtabs %}

