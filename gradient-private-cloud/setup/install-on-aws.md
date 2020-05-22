# Install on AWS

For AWS, the Gradient installer will utilize Terraform to provision a Elastic Kubernetes Service \(EKS\) cluster. You must follow the [pre-installation steps](pre-installation-steps.md) before continuing.

#### Requirements

There are many ways of passing in your credentials in order for Terraform to authenticate with your cloud provider. Most likely, you already have your cloud provider credentials loaded through the AWS CLI. Terraform will automatically detect those credentials during initialization for you. See [configuring the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) for more information on setting up credentials and user profiles. The AWS user that's responsible for Gradient installation must have broad read/write privileges across services – ideally administrative privileges in the account.

{% hint style="info" %}
Do not remove the user later or you will lose access to the cluster.
{% endhint %}

You will also need to have `aws-iam-authenticator` installed on the computer or instance where you plan to run the installer. [https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

#### General Configuration

Next you should create a file in the gradient-cluster folder you created – the file must be named `main.tf` and should contain the text in the box below \(note the copy icon in the upper right corner\).

Be sure to replace the following fields with the appropriate values:

* name \(the same name used when registering the new cluster in the Paperspace web console\)
* aws\_region \(your preferred AWS region\)
* artifacts\_access\_key\_id \(the key for the bucket that was set up for artifacts storage\)
* artifacts\_path \(the full s3 path to the bucket\)
* artifacts\_secret\_access\_key
* cluster\_apikey \(provided during registration of the new cluster\)
* cluster\_handle \(provided during registration of the new cluster\)
* domain \(same as what was entered during cluster registration\)

#### SSL Configuration

The Gradient installer can use Let's Encrypt to create a SSL certificate, verify it by making entries with your DNS provider, and install the certificate on your cluster to secure access to notebooks, model deployments, etc. For this to work, your domains DNS provider must be [on the supported list](lets-encrypt-dns-providers.md). To use this functionality, create a block in your `main.tf` file similar to the one in the example below. Use the `letsencrypt_dns_name` that matches your provider in the list, and provide the required authentication field\(s\) as specified in the `letsencrypt_dns_settings` column.

If you don't want to use automatic SSL, use `tls_cert` and `tls_key` entries and be sure the SSL certificate files are located in the directory and filenames specified \(or change them in the `main.tf` file\).

You can use either the Let's Encrypt block OR the manual certificate block, but not both.

#### main.tf file example

```text
module "gradient_aws" {
    source = "github.com/paperspace/gradient-installer?ref=master/gradient-aws"

    // name should only have letters, numbers, and dashes
    name = "cluster-name"
    aws_region = "us-east-1"

    artifacts_access_key_id = "artifacts-access-key-id"
    artifacts_path = "s3://artifacts-bucket"
    artifacts_secret_access_key = "artifacts-secret-access-key"
    
    cluster_apikey = "cluster-apikey-from-paperspace-com"
    cluster_handle = "cluster-handle-from-paperspace-com"
    domain = "gradient.mycompany.com"

    // insert a SSL block below - the first example is for Cloudflare DNS
    
    /*
    letsencrypt_dns_name = "cloudflare"
    letsencrypt_dns_settings = {
        CF_API_KEY = "[Global cloudflare key]"
        CF_API_EMAIL = "[Cloudflare email address]"
    }
    */

    // or disable automatic SSL by specifying cert files below
    // tls_cert = file("./certs/ssl-bundle.crt")
    // tls_key = file("./certs/ssl.key")
}

output "ELB_HOSTNAME" {
    value = module.gradient_aws.elb_hostname
}
```

#### Installation

Next, install Gradient using Terraform:

```text
terraform init
terraform apply
```

The init step should take less than a minute, and the apply step may take 15 minutes or more. At the end of the apply step, the installer will return the AWS hostname of the load balancer in your new cluster. 

Gradient requires two DNS CNAME records to make external services accessible. Use the hostname of the load balancer as the target for these records, as shown below.

Example:

`*.gradient.mycompany.com [ELB_HOSTNAME]`

`gradient.mycompany.com [ELB_HOSTNAME]`

#### Hot nodes

By default, hot nodes are set up for experiments, model deployments, notebooks, and tensorboards on one c5.xlarge instance each. 

Hot nodes can be reconfigured by setting k8s\_node\_asg\_min\_sizes in the main.tf file similar to the example below.

```text
  k8s_node_asg_min_sizes = {
        "experiment-cpu-small"=1,
        "experiment-cpu-medium"=0,
        "experiment-gpu-small"=0,
        "experiment-gpu-medium"=0,
        "experiment-gpu-large"=0

        "model-deployment-cpu-small"=1,
        "model-deployment-cpu-medium"=0,
        "model-deployment-gpu-small"=0,
        "model-deployment-gpu-medium"=0,
        "model-deployment-gpu-large"=0

        "notebook-cpu-small"=1,
        "notebook-cpu-medium"=0,
        "notebook-gpu-small"=0,
        "notebook-gpu-medium"=0,
        "notebook-gpu-large"=0,

        "tensorboard-cpu-small"=1,
        "tensorboard-cpu-medium"=0,
        "tensorboard-gpu-small"=0,
        "tensorboard-gpu-medium"=0,
        "tensorboard-gpu-large"=0
  }
```



#### Managing the Kubernetes cluster with KUBECONFIG

For those familiar with Kubernetes, a file will be generated in the gradient-cluster folder that contains the Kubernetes `kubeconfig`. To use the generated KUBECONFIG, AWS requires aws-iam-authenticator to be installed: [https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

Managing the Kubernetes cluster manually is not required to use Gradient.

#### Updating the Gradient cluster

To update Gradient, run `terraform apply` from the gradient-cluster folder.

#### Uninstalling Gradient

Uninstallation can be handled by Terraform by running: `terraform destroy`



