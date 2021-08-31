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

For AWS S3 you can define a bucket using the AWS CLI.  Here we create a bucket named `my-gradient-storage-provider-bucket`.
```
aws s3api create-bucket --bucket my-gradient-storage-provider-bucket --region us-east-1
```

Gradient will create folders and objects inside this bucket, once configured.

## Configure your storage bucket

From within a new or existing S3 bucket, you'll need to edit the CORS configuration so your data can be viewed within Gradient.

As a best practice you should create a dedicated user identity and access key/secret key pair for accessing the bucket. You should also set a restricted access policy on the user identity so it is limited this bucket.

**Assign CORS Rules**

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

In the AWS S3 console bucket _permissions_ settings, you'll see an option to edit the CORS configuration. Click edit, then copy and paste the JSON above, and then save your changes.

![](../../../.gitbook/assets/image%20%28108%29.png)

Alternatively you can apply them using the AWS CLI:
```
aws s3api put-bucket-cors --bucket my-gradient-storage-provider-bucket --cors-configuration '{
  "CORSRules": [
    {
      "AllowedHeaders": ["*"],
      "AllowedMethods": ["GET", "PUT"],
      "AllowedOrigins": ["https://console.paperspace.com"],
      "MaxAgeSeconds": 3000
    }
  ]
}'
```

**Create a Restricted User and Access Key/Secret Key**

Create a restricted user identity and access key/secret key for accessing the bucket.

Here we create these using the AWS CLI:
```
aws iam create-user --user-name gradient-storage-provider-user

aws iam create-access-key --user-name gradient-storage-provider-user
```
Note the returned `AccessKeyId` and `SecretAccessKey` values as they will only appear once.

**Create Bucket Access Policy**

Gradient requires a minimal level of policy permissions to access the bucket. Sample permissions for a bucket named `my-gradient-storage-provider-bucket` are as follows:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowGeneratedUrls",
            "Effect": "Allow",
            "Action": "sts:GetFederationToken",
            "Resource": "*"
        },
        {
            "Sid": "AllowListBucket",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::my-gradient-storage-provider-bucket"
        },
        {
            "Sid": "AllowBucketAccess",
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::my-gradient-storage-provider-bucket/*"
        }
    ]
}
```
Customize the above policy definition for your specific bucket name in the `AllowListBucket` and `AllowBucketAccess` **Resource** fields.
Place the policy definition in a file, e.g, `gradient-storage-provider-access-policy.json`.

**Create Policy**

Using the AWS CLI create a policy object from the policy definition file:
```
aws iam create-policy --policy-name gradient-storage-provider-access-policy \
  --policy-document file://gradient-storage-provider-access-policy.json
```
Note the returned policy `"Arn"` value, which is used when assigning the policy to the user identity.

**Attach Policy to User**

Attach the policy object to the restricted user identity.

Using the AWS CLI:
```
aws iam attach-user-policy --user-name gradient-storage-provider-user \
  --policy-arn "arn:aws:iam::XXXXXXXXXXXX:policy/gradient-storage-provider-access-policy"
```

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

