# Storage Providers

Storage providers are a way to connect various storage resources to Gradient. Once connected this storage can be used to store and access data for use in Gradient, such as models, artifacts, and datasets. Gradient uses storage providers with [**Versioned Datasets**](https://docs.paperspace.com/gradient/data/data-overview/private-datasets-repository) to ensure that your data is verified and immutable. Gradient will create a folder with the same name as your Paperspace team ID within the storage provider. Gradient storage providers do not provide general S3 capabilities through the storage provider interface. However if you define additional storage providers, you can use the tools compatible with your storage provider to interact with the data stored by Gradient.

## Gradient Managed Storage Provider

Your Gradient account automatically comes with a storage provider named **Gradient Managed**. This storage provider can be used without additional configuration, for storing data in Gradient's hosted s3 compatible object storage.

**Gradient Managed** storage has a default persistent storage quota, based on your Gradient subscription level, which can be used for no additional charges. After the default quota is consumed you may need to upgrade your subscription plan to have access to more. See your [**Gradient Subscription plan**](https://gradient.paperspace.com/pricing) details for more info.

## Setting up additional Storage Providers

Choose a public storage provider, such as AWS S3, Google GCS, minio, or similar. Currently Gradient supports these types of storage providers:

**Supported types:**

* S3-compatible storage

## Define a storage bucket

Create a bucket within your storage provider, and a set of read/write credentials for accessing the data \(usually an access key and secret key\). Note the bucket name, and endpoint url, as well as access key and secret key.

Gradient will create folders and objects inside this bucket, once configured.

## Configure your storage bucket

From within a new or existing S3 bucket, you'll need to edit the CORS configuration so your data can be viewed within Gradient.

**CORS**

Add CORS rules to your bucket:

```text
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "PUT"
        ],
        "AllowedOrigins": [
            "https://console.paperspace.com"
        ],
        "ExposeHeaders": [],
        "MaxAgeSeconds": 3000
    }
]
```

Within the bucket _permissions_ settings, you'll see an option to edit the CORS configuration. Click edit, then copy and paste the JSON above, and then save your changes.

![](../../../.gitbook/assets/image%20%28108%29.png)

## Add a Storage Provider

A Storage Provider can be created on your team's settings page.

![](../../../.gitbook/assets/screen-shot-2020-10-30-at-1.09.41-pm.png)

**Note:** The "AccessKey" and "SecretAccessKey" can be obtained from the "My security credentials" section of the AWS Identity and Access Management \(IAM\) portal. See the following:

![](../../../.gitbook/assets/image%20%28109%29.png)

### CLI

A Storage Provider can also be created with the Gradient CLI

```text
$ gradient storageProviders create s3 --name test --bucket my-bucket --accessKey=access-key --secretAccessKey=secret-key
Created storage provider: splgct3arqdh77c
```

