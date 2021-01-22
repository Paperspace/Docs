# Storage Providers

Storage providers are a way to connect storage to Gradient. Gradient manages this storage provider to ensure that your data is verified and immutable. Gradient will create a folder with your Paperspace team handle at this storage provider. Gradient does not provide general s3 capabilities through the storage provider interface it is merely a way to manage credentials and the storage of specific Gradient features such as models, notebook workspaces and datasets currently only available on private and managed clusters.

**Supported types:**

* S3-compatible storage

## Configure your storage bucket

From within a new or existing S3 bucket, you'll need to edit the CORS configuration so your data can be viewed within Gradient.

**CORS**

To access an S3 compatible storage provider you may have to add CORS rules to your bucket

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

![](../.gitbook/assets/image%20%28108%29.png)

## Create the Storage Provider

A Storage Provider can be created on your team's settings page.

![](../.gitbook/assets/screen-shot-2020-10-30-at-1.09.41-pm.png)

**Note:** The "AccessKey" and SecretAccessKey" can be obtained from the "my security credentials" section of the AWS Identity and Access Management \(IAM\) portal. See the following:

![](../.gitbook/assets/image%20%28109%29.png)

### CLI

A Storage Provider can also be created with the Gradient CLI

```text
$ gradient storageProviders create s3 --name test --bucket my-bucket --accessKey=access-key --secretAccessKey=secret-key
Created storage provider: splgct3arqdh77c
```

