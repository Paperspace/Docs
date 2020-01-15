# Datasets

## About

When executing an experiment in Gradient you may optionally supply one or more datasets that will be downloaded into your experiment's environment prior to execution.
These datasets can be downloaded from an S3 object or folder (including the full bucket).
Gradient allows teams to run reproducible machine learning experiments by taking advantage of S3 ETags and Version IDs, which combine to allow you to be sure that datasets exactly match between training sets, and to be sure which version of a dataset you are using.

## S3 Datasets

Datasets are downloaded and mounted readonly on `/data/DATASET` within your experiment jobs using the supplied AWS credentials.
The credentials are optional for public buckets.
The name of the dataset is the `basename` of the last item in the s3 path, e.g. `s3://my-bucket/mnist.zip` would have the name `mnist` and `s3://my-bucket` would have the name `my-bucket`.
The name maybe overridden with the optional `name` parameter.

For example these flags would be added to an experiment `run` cli command.

```
  --datasetUri "s3://bucket-name/my-dataset.zip" \
  --datasetName "dataset A" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555"
```

### ETag

When downloading a dataset you may supply an optional `etag` parameter, which will tell the dataset downloader to verify that the object stored at the path matches the supplied etag.
If it does not match the etag, the experiment will end with an error.
This feature is only supported on S3 objects and not buckets.

For example these flags would be added to an experiment `run` cli command.

```
  --datasetUri "s3://bucket-name/my-dataset.zip" \
  --datasetName "dataset A" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555" \
  --datasetEtag "3823e4ab23cc48ad83e9e3fa99ecc12a"
```

### VersionId

When downloading a dataset you may supply an optional `versionId` parameter, which will tell the dataset downloader to fetch your S3 object at the specified version.
This feature is only supported on versioned S3 buckets and is not supported on downloads of folders.

For example these flags would be added to an experiment `run` cli command.

```
  --datasetUri "s3://bucket-name/my-dataset.zip" \
  --datasetName "dataset A" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555" \
  --datasetVersionId "bjh023v9dloWEq23VC912zxprrl8.23C" \
```

#### Downloading to Shared Storage

Datasets are downloaded to team shared storage by default storage per experiment job.
This will download the dataset to a unique path within your shared storage and mount it into your experiment jobs at the same path as if you had downloaded it to a dynamic volume.
This can be useful for quickly switching your volume options without changing your experiment code.
It is *strongly* recommended to supply an etag for shared storage downloads to ensure that you have a consistent dataset between experiment executions.

For example,

```
  --datasetUri "s3://bucket-name/my-dataset.zip" \
  --datasetName "dataset A" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555" \
  --datasetEtag "3823e4ab23cc48ad83e9e3fa99ecc12a"
```

### Using Dynamic Volumes

When downloading a dataset they are by default downloaded to shared storage.
This means that for a 3 worker, 2 parameter server experiment the dataset will be downloaded 5 times.
This is a good option for when you do not want your datasets to be persisted against your shared storage quota, or are small or frequently changing datasets.
If you would prefer for your datasets to be downloaded to an ephemeral location you can specify a `volumeKind` of `dynamic`.
These volumes are 5 GB (`"5Gi"`) by default; if you need a larger volume you may supply a size parameter with your dataset.

For example, this snippet will start an experiment with a dataset that downloads to a 10 GB volume:

```
  --datasetUri "s3://bucket-name/my-dataset.zip" \
  --datasetName "dataset A" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555" \
  --datasetVersionId "bjh023v9dloWEq23VC912zxprrl8.23C" \
  --datasetVolumeKind "dynamic" \
  --datasetVolumeSize "10Gi"
```

Size units may be specified with the SI prefix for base-10 units (K, M, G, T).
Or for base-2 quantities you may add an `i` specifier at the end (Ki, Mi, Gi, Ti).

#### Cleaning Up Shared Storage

Because shared storage datasets are stored in your team storage they are not automatically deleted.
Notebooks and experiments both mount the raw datasets with unique disambiguated names under `/storage/data` and you can use these tool to manually clean up old datasets.
The datasets under `/storage/data/` will be named `<DATASET_NAME-ETAG-VERSIONID>`, where `DATASET_NAME` is derived from the bucket (`basename` on the key name) or the user supplied name parameter.
If the dataset was downloaded without an `etag`, the `-ETAG` portion of the download path is omitted.
If the dataset was downloaded without an `versionId`, the `-VERSIONID` portion of the download path is omitted.

#### Archive Expansion

If the object supplied is in a recognized archive format, such as zip, the archive will automatically be expanded in the root of the mount path.
For example, `s3://my-bucket/dataset.zip` would be downloaded and expanded so that the contents of `dataset.zip` are accessible inside the container at `/data/dataset`.
Archive formats are detected by their extension. These are the supported archive extensions:
* .zip
* .tar
* .tar.bz2
* .tar.gz
* .tar.gz2
* .tar.xz
* .tbz
* .tbz2
* .tgz
* .txz

### Using Datasets with Gradient CLI

The following options specify datasets on the command line. For all optional options,
specify a value of `"none"` to indicate no value for that option. For any `datasetUri`
which specifies a directory, the `datasetVersionId` and `datasetEtag` are ignored.

<table>
  <thead>
    <tr>
      <th style="text-align:left">CLI Option</th>
      <th style="text-align:left">SDK Field</th>
      <th style="text-align:left">Optional?</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <code>--datasetUri</code>
      </td>
      <td style="text-align:left">
        <code>url</code>
      </td>
      <td style="text-align:left">
        No
      </td>
      <td style="text-align:left">
        Dataset URL
      </td>
      <td style="text-align:left">
        <code>"s3://bucket-name/my-dataset.zip"</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <code>--datasetName</code>
      </td>
      <td style="text-align:left">
        <code>name</code>
      </td>
      <td style="text-align:left">
        Yes
      </td>
      <td style="text-align:left">
        Dataset display name
      </td>
      <td style="text-align:left">
        <code>"dataset A"</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <code>--datasetAwsAccessKeyId</code>
      </td>
      <td style="text-align:left">
        <code>awsAccessKeyId</code>
      </td>
      <td style="text-align:left">
        No
      </td>
      <td style="text-align:left">
        AWS Access Key ID for the <code>datasetUri</code>
      </td>
      <td style="text-align:left">
        <code>"ABCDEFGHIJ0123456789"</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <code>--datasetAwsSecretAccessKey</code>
      </td>
      <td style="text-align:left">
        <code>awsSecretAccessKey</code>
      </td>
      <td style="text-align:left">
        No
      </td>
      <td style="text-align:left">
        AWS Secret Access Key paired with the <code>datasetAwsAccessKeyId</code>
      </td>
      <td style="text-align:left">
        <code>"aaaabbbbccccddddeeee11112222333344445555"</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <code>--datasetVersionId</code>
      </td>
      <td style="text-align:left">
        <code>versionId</code>
      </td>
      <td style="text-align:left">
        Yes
      </td>
      <td style="text-align:left">
        AWS S3 object version ID of the object specified in the <code>datasetUri</code>
      </td>
      <td style="text-align:left">
        <code>"bjh023v9dloWEq23VC912zxprrl8.23C"</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <code>--datasetEtag</code>
      </td>
      <td style="text-align:left">
        <code>etag</code>
      </td>
      <td style="text-align:left">
        Yes
      </td>
      <td style="text-align:left">
        AWS S3 object etag of the object specified in the <code>datasetUri</code>
      </td>
      <td style="text-align:left">
        <code>"3823e4ab23cc48ad83e9e3fa99ecc12a"</code>
      </td>
    </tr>
  </tbody>
</table>

The following command runs an experiment with the above example values for a dataset:

```bash
gradient experiments run singlenode \
  --projectId <your-project-id> \
  --name singleEx \
  --experimentEnv "{\"EPOCHS_EVAL\":5,\"TRAIN_EPOCHS\":10,\"MAX_STEPS\":1000,\"EVAL_SECS\":10}" \
  --container tensorflow/tensorflow:1.13.1-gpu-py3 \
  --machineType K80 \
  --command "python mnist.py" \
  --workspaceUrl https://github.com/Paperspace/mnist-sample.git \
  --modelType Tensorflow \
  --modelPath /artifacts \
  --datasetUri "s3://bucket-name/my-dataset.zip" \
  --datasetName "dataset A" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555" \
  --datasetVersionId "bjh023v9dloWEq23VC912zxprrl8.23C" \
  --datasetEtag "3823e4ab23cc48ad83e9e3fa99ecc12a"
```

Multiple datasets may be specified by specifying more sets of **all of the `dataset` options**.
Each `dataset` option must be specified for each dataset.
Consider the following 3 datasets:

1. Name: Dataset A
    - URI: s3://bucket-name/my-dataset.zip
    - AWS Access Key ID: ABCDEFGHIJ0123456789
    - AWS Secret Access Key: aaaabbbbccccddddeeee11112222333344445555
    - Version ID: bjh023v9dloWEq23VC912zxprrl8.23C
    - ETag: 3823e4ab23cc48ad83e9e3fa99ecc12a
2. Name: Dataset B
    - URI: s3://bucket-name/dataset-dir/
    - AWS Access Key ID: ABCDEFGHIJ0123456789
    - AWS Secret Access Key: aaaabbbbccccddddeeee11112222333344445555
    - Version ID: None
    - ETag: None
3. Name: Dataset C
    - URI: s3://another-bucket/another-dataset.zip
    - AWS Access Key ID: KLMNOPQRST0123456789
    - AWS Secret Access Key: eeeeddddccccbbbbaaaa11112222333344445555
    - Version ID: 9Jqci387dcb8dekdm39ckbhs8nAS8cVV
    - ETag: None

A command which utilizes all of those datasets looks like the following:

```bash
gradient experiments run singlenode \
  --projectId <your-project-id> \
  --name singleEx \
  --experimentEnv "{\"EPOCHS_EVAL\":5,\"TRAIN_EPOCHS\":10,\"MAX_STEPS\":1000,\"EVAL_SECS\":10}" \
  --container tensorflow/tensorflow:1.13.1-gpu-py3 \
  --machineType K80 \
  --command "python mnist.py" \
  --workspaceUrl https://github.com/Paperspace/mnist-sample.git \
  --modelType Tensorflow \
  --modelPath /artifacts \
  --datasetUri "s3://bucket-name/my-dataset.zip" \
  --datasetName "dataset A" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555" \
  --datasetVersionId "bjh023v9dloWEq23VC912zxprrl8.23C" \
  --datasetEtag "3823e4ab23cc48ad83e9e3fa99ecc12a" \
  --datasetUri "s3://bucket-name/dataset-dir" \
  --datasetName "dataset B" \
  --datasetAwsAccessKeyId "ABCDEFGHIJ0123456789" \
  --datasetAwsSecretAccessKey "aaaabbbbccccddddeeee11112222333344445555" \
  --datasetVersionId "none" \
  --datasetEtag "none" \
  --datasetUri "s3://another-bucket/another-dataset.zip" \
  --datasetName "dataset C" \
  --datasetAwsAccessKeyId "KLMNOPQRST0123456789" \
  --datasetAwsSecretAccessKey "eeeeddddccccbbbbaaaa11112222333344445555" \
  --datasetVersionId "9Jqci387dcb8dekdm39ckbhs8nAS8cVV" \
  --datasetEtag "none"
```
