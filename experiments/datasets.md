# Datasets

## About

When executing an experiment in Gradient you may optionally supply one or more datasets that will be downloaded into your experiment's environment prior to execution.
These datasets can be downloaded from an S3 object or folder (including the full bucket).
Gradient allows teams to run reproducible machine learning experiments by taking advantage of S3 ETags and Version IDs, which combine to allow you to be sure that datasets exactly match between training sets, and to be sure which version of a dataset you are using.

## S3 Datasets

Datasets are downloaded and mounted readonly on `/data/global/DATASET` within your experiment jobs using the supplied AWS credentials.
The credentials are optional for public buckets.
The name of the dataset is the `basename` of the last item in the s3 path, e.g. `s3://my-bucket/mnist.zip` would have the name `mnist` and `s3://my-bucket` would have the name `my-bucket`.
The name maybe overridden with the optional `name` parameter.

```
datasets: [
    {
        "url": "s3://my-bucket/mnist-modified.zip",
        "awsSecretAccessKey": "<KEY>",
        "awsAccessKeyId": "<ID>",
        "name": "mnist",
    },
]
```

### ETag

When downloading a dataset you may supply an optional `etag` parameter, which will tell the dataset downloader to verify that the object stored at the path matches the supplied etag.
If it does not match the etag, the experiment will end with an error.
This feature is only supported on S3 objects and not buckets.

```
datasets: [
    {
        "url": "s3://my-bucket/my-dataset.zip",
        "awsSecretAccessKey": "<KEY>",
        "awsAccessKeyId": "<ID>",
        "etag": "d0e2243df4d1e89ead52d51083b2eb523593b38e",
    },
]
```

### VersionId

When downloading a dataset you may supply an optional `versionId` parameter, which will tell the dataset downloader to fetch your S3 object at the specified version.
This feature is only supported on versioned S3 buckets and is not supported on downloads of folders.

```
datasets: [
    {
        "url": "s3://my-bucket/my-dataset.zip",
        "awsSecretAccessKey": "<KEY>",
        "awsAccessKeyId": "<ID>",
        "versionId": "1111111",
    },
]
```

### Supplying a Different Volume Size

When downloading a dataset they are by default downloaded to an ephemeral volume that lasts for the duration of the experiment job.
These volumes are 5 GB (`"5Gi"`) by default; if you need a larger volume you may supply a size parameter with your dataset.

For example, this snippet will start an experiment with a dataset that downloads to a 10 GB volume:

```
datasets: [
    {
        "url": "s3://my-bucket/my-dataset.zip",
        "awsSecretAccessKey": "<KEY>",
        "awsAccessKeyId": "<ID>",
        "volumeOptions": {
            "kind": "dynamic",
            "size": "10Gi",
        },
    },
]
```

Size units may be specified with the SI prefix for base-10 units (K, M, G, T).
Or for base-2 quantities you may add an `i` specifier at the end (Ki, Mi, Gi, Ti).

#### Downloading to Shared Storage

Datasets are normally downloaded to transient storage per experiment job.
This means that for a 3 worker, 2 parameter server experiment the dataset will be downloaded 5 times.
Since this can be very inefficient, in order to decrease job start up time you may choose to download your artifact to your team shared storage space.
This will download the dataset to a unique path within your shared storage and mount it into your experiment jobs at the same path as if you had downloaded it to a dynamic volume.
This can be useful for quickly switching your volume options without changing your experiment code.
It is *strongly* recommended to supply an etag for shared storage downloads to ensure that you have a consistent dataset between experiment executions.

For example,

```
datasets: [
    {
        "url": "s3://my-bucket/my-dataset.zip",
        "awsSecretAccessKey": "<KEY>",
        "awsAccessKeyId": "<ID>",
        "etag": "d0e2243df4d1e89ead52d51083b2eb523593b38e",
        "volumeOptions": {
            "kind": "shared",
        },
    },
]
```

#### Cleaning Up Shared Storage

Because shared storage datasets are stored in your team storage they are not automatically deleted.
Datasets are downloaded to `/<TEAMHANDLE>/data/<DATASET_NAME-ETAG>`, where `DATASET_NAME` is derived from the bucket or the user supplied parameter.
If the dataset was downloaded without an `etag`, the `-ETAG` portion of the download path is omitted.

#### Archive Expansion

If the object supplied is in a recognized archive format, such as zip, the archive will automatically be expanded in the root of the mount path.
For example, `s3://my-bucket/dataset.zip` would be downloaded and expanded so that the contents of `dataset.zip` are accessible inside the container at `/data/global/dataset`.
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
