# Pre-installation steps

## Create gradient-cluster directory for your Terraform configuration

On your local computer, create a directory called `gradient-cluster` for your Gradient cluster Terraform files. You'll soon run Terraform from there to create your Gradient cluster during the main installation process. You'll be provided a configuration that will call out to [gradient-installer](https://github.com/Paperspace/gradient-installer) to create and install Gradient – you do _not_ need to clone down gradient-installer or run it directly.

## Create Terraform provider file in S3 \(optional\)

To maintain Terraform state in a shared location \(recommended\), create a `backend.tf` file in your gradient-cluster directory with the following Terraform configuration code:

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

Suggestion: replace `artifacts-bucket` above with the name of the artifacts storage bucket you created – that way your Terraform state will be stored in the same S3 bucket as your Gradient job artifacts.

Note: using a S3 bucket for shared state will require the ability to access a S3 bucket during Terraform runs. This means you'll need to have the aws-cli installed and appropriate credentials in place to access the bucket.

