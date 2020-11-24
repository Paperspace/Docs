# Storage Providers

Storage providers are a way to connect storage to Gradient. Gradient manages this storage provider to ensure that your is data verified and immutable. Gradient will create a folder with your Paperspace team handle at this storage provider.

**Supported types:**

* S3-compatible storage

## Setup a storage provider

**CORS**

To access an S3 compatible storage provider you may have to add CORS rules to your bucket

```text
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>https://console.paperspace.com</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <MaxAgeSeconds>3000</MaxAgeSeconds>
    <AllowedHeader>*</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```

A Storage Provider can be created on your team's setting's page.

![](../.gitbook/assets/screen-shot-2020-10-30-at-1.09.41-pm.png)

#### CLI

A Storage Provider can also be created with the Gradient CLI

```text
$ gradient storageProviders create s3 --name test --bucket my-bucket --accessKey=access-key --secretAccessKey=secret-key
Created storage provider: splgct3arqdh77c
```

