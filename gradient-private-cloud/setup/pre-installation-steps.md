# Pre-installation steps

There's several steps that are common to all installed environments, and these are listed below. After completing these steps you'll find links to individual steps for AWS and other cloud/VM/bare metal environments. 

#### Pre-install - artifacts storage

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

Next, create a dedicated IAM user for read/write access to the S3 bucket with the following policy:

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
            "Sid": "AllowListbucket",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::[bucket_name]"
        },
        {
            "Sid": "AllowBucketAccess",
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::[bucket]/*"
        }
    ]
}
```

On the user's Security Credentials tab, create an access key for this user, which will be used when registering your cluster in the Paperspace web console.

#### Pre-install - cluster registration

Next, you'll need to register a new cluster in the [Paperspace web console](https://www.paperspace.com/console/clusters). After you've registered a cluster you'll be provided an API key and cluster handle, which, along with the cluster name you provided, will be used later in the install process.  

#### Pre-install - SSL certificate 

Gradient uses a wildcard SSL certificate to secure HTTP traffic into your processing site. The installer can provide an automatic certificate or you can also provide your own. 

If you decide to provide your own SSL certificate, you will need two files: one private key file and one .crt file that contains your entire certificate chain including any root or intermediate certificates. \(Example: [https://support.comodo.com/index.php?/Knowledgebase/Article/View/1145/1/how-do-i-make-my-own-bundle-file-from-crt-files](https://support.comodo.com/index.php?/Knowledgebase/Article/View/1145/1/how-do-i-make-my-own-bundle-file-from-crt-files)\)

Example:

* \*.gradient.mycompany.com

#### Create gradient-cluster folder 

On your local computer create a folder named gradient-cluster

#### Create Terraform provider file \(optional\)

To maintain Terraform state in a shared location, you should create a file in the gradient-cluster folder called: `backend.tf` with the information below \(you can replace `artifacts-bucket` with the name of the artifacts storage bucket you created – that way your Terraform state will be stored in the same S3 bucket as your Gradient job artifacts\).

```text
terraform {
    backend "s3" {
        bucket = "artifacts-bucket"
        key    = "gradient-processing"
        region = "us-east-1"
        session_name = "gradient-processing-terraform"
    }
}
```

Note that using a S3 bucket for shared state will require the ability to access a S3 bucket during Terraform runs. This means you'll need to have the aws-cli installed and appropriate credentials in place to access the bucket. 

