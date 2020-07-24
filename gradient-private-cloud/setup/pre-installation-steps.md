# Pre-installation steps

## 1. Setup artifact storage

Create an AWS S3 bucket for artifacts. Next, add CORS permissions to the bucket you created:

```text
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>https://www.paperspace.com</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <MaxAgeSeconds>3000</MaxAgeSeconds>
    <AllowedHeader>*</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```

To add these permissions, navigate to the S3 bucket settings in the AWS console, then select the Permissions tab and the CORS Configuration button:

![](../../.gitbook/assets/s3_management_console%20%281%29.png)

Next, create a dedicated IAM user with Programmatic Access for read/write access to the S3 bucket with the following policy:

```text
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
            "Resource": "arn:aws:s3:::[bucket_name]"
        },
        {
            "Sid": "AllowBucketAccess",
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::[bucket_name]/*"
        }
    ]
}
```

On the user's Security Credentials tab, create an access key for this user, which will be used when registering your cluster in the Paperspace web console.



## 2. SSL

Gradient uses a wildcard SSL certificate to secure HTTP traffic into your processing site. The installer can provide an automatic certificate if you have a supported DNS provider \([supported DNS providers](lets-encrypt-dns-providers.md)\) or you can provide your own.

If you decide to provide your own SSL certificate, you will need two files: one private key file and one .crt file that contains your entire certificate chain including any root or intermediate certificates. \(Example: [https://support.comodo.com/index.php?/Knowledgebase/Article/View/1145/1/how-do-i-make-my-own-bundle-file-from-crt-files](https://support.comodo.com/index.php?/Knowledgebase/Article/View/1145/1/how-do-i-make-my-own-bundle-file-from-crt-files)\)

Example:

* `*.gradient.mycompany.com`

