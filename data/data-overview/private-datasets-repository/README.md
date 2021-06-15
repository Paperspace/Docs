# Versioned Data

### Overview

Versioned Datasets are used to manage the flow of data with your machine learning workloads. Datasets have immutable versions that can be used to track your data as it changes. Dataset version can be used as input to Gradient workloads as well as outputs. Data is stored at a [Storage Provider](storage-providers.md) and will be cached on a Gradient cluster's shared storage for a period of time so that data will be available readily on repeated usage.

{% hint style="info" %}
Gradient datasets require a private [Gradient Cluster](../../../gradient-private-cloud/about/).
{% endhint %}

### Versions, Tags, and Messages

Datasets have multiple versions that can be referenced. You can specify a message with a new dataset version to provide info around a newly created dataset version. In addition, you can tag a specific dataset version with a custom name as well. Here are the available ways to reference a dataset:

* `[dataset-id]:latest` : this will use the latest version of your dataset
* `[dataset-id]:[dataset-version]`: this will the use the specified dataset-version
* `[dataset-id]:[dataset-tag]` : this will use the specified  dataset version that the dataset-tag points to

### Committed state

Dataset versions have an uncommitted and committed state. When a Dataset is uncommitted, you can modify or add files freely. When a Dataset is committed it will be immutable \(will not allow any modifications\). This allows workloads to be repeatable and deterministic with the provided Datasets.

## Creating a Dataset and Dataset Version

{% tabs %}
{% tab title="GUI" %}
To create a new dataset \(one that does not yet have an ID\) in the GUI, go to the Data tab in your team's page and click "Create a Dataset". This brings up a window to give it a name, optional description, and select the storage provider on which it will be created.

![Creation of new dataset](../../../.gitbook/assets/image%20%2874%29.png)

If the team already has datasets, there is a similar "Add" button. The resulting screen after creation allows you to upload files, or you can just retrieve the dataset ID for use elsewhere.

![Optional importing of data](../../../.gitbook/assets/image%20%2860%29.png)

Importing data, or adding it in some other way such as a Workflow output, will create a new version of the dataset.
{% endtab %}

{% tab title="CLI" %}
To create a new dataset \(one that does not yet have an ID\) in the CLI, use gradient datasets create with a command like

```text
$ gradient datasets create --name democli --storageProviderId ssfe843ndkjdsnr
Created dataset: dsr5zdx0thjhfe2
```

To create a new dataset version, use, e.g.,

```text
$ gradient datasets versions create --id=dst364npcw6ccok --source-path=./some-data/
Created dataset version: dst364npcw6ccok:fo5rp4m
Committed dataset version: dst364npcw6ccok:fo5rp4m
```
{% endtab %}
{% endtabs %}

## Using Datasets

You can use existing Datasets or create new ones. In the below scenarios, the following dataset actions are specified:

* **dst123abc:latest** will be mounted to: **/inputs/my-dataset**

```yaml
job-1:
  inputs:
    my-dataset:
      type: dataset
      with:
        ref: dst123abc
   uses: container@v1
   with:
    image: bash:5
    args: ["bash", "-c", "ls /inputs/my-dataset"]
```

* **dst123abc:latest** will be created by job-1 and mounted to job-2 at: **/inputs/my-created-dataset**

```yaml
job-1:
  outputs:
    my-dataset:
      type: dataset
      with:
        ref: dst123abc
  uses: container@v1
  with:
    image: bitnami/git
    args: ["bash", "-c", "git clone https://github.com/username/repo /outputs/my-dataset"]
job-2:
  needs:
    - job-1
  inputs:
    my-created-dataset: job-1.outputs.my-dataset
  uses: container@v1
    with:
      image: bash:5
      args: ["bash", "-c", "ls /inputs/my-created-dataset"]
```

## Viewing Datasets

```text
$ gradient datasets list
+------+-----------------+-------------------------+
| Name | ID              | Storage Provider        |
+------+-----------------+-------------------------+
| test | dst364npcw6ccok | test1 (splgct3arqdh77c) |
+------+-----------------+-------------------------+

$ gradient datasets details --id=dst364npcw6ccok
+-----------------+-------------------------+
| Name            | test                    |
+-----------------+-------------------------+
| ID              | dst364npcw6ccok         |
| Description     |                         |
| StorageProvider | test1 (splgct3arqdh77c) |
+-----------------+-------------------------+
```

## Viewing Dataset files

```text
$ gradient datasets files list --id=dst364npcw6ccok:fo5rp4m
+-----------+------+
| Name      | Size |
+-----------+------+
| hello.txt | 12   |
+-----------+------+
```

