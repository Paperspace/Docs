# Install on NVIDIA DGX

This version should be used for NVIDIA DGX-1 hosts. Terraform, running inside a Docker container, will be used to provision a Kubernetes cluster on the hosts and will require ssh access to all hosts in order to connect. Note that in this scenario auto-scaling is not available – all nodes will be running at all times.

Be sure to follow the [pre-installation steps](../pre-installation-steps.md), and then run this:

```text
mkdir gradient-cluster
ssh-keygen -f gradient-cluster/gradient_rsa
```

#### Requirements

On the computer where you plan to run the Gradient installer, you must have Docker installed with a user that has access to /var/run/docker.sock.

For the NVIDIA DGX-1 hosts:

* Ubuntu 18.04
* NFS server available to all nodes
* Docker installed on all hosts \(or use `"setup_docker = true"` in the main.tf file below to have Docker installed during install\)
* Set default docker runtime to nvidia in /etc/docker/daemon.json \(or set `"setup_nvidia = true"` in the main.tf file, below\): 

```text
{
    "default-runtime": "nvidia",
    "runtimes": {
        "nvidia": {
            "path": "/usr/bin/nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}
```

The above is an example of how the added line appears in the JSON file. Do not remove any pre-existing content when making this change.

* Ensure your SSH user has access to the docker group in /etc/group:

```text
docker:x:999:ubuntu
```

* Ensure the SSH public key that was generated above is installed on each host
* Ensure sudo is enabled for the account you're logging into
* Ensure /etc/sshd/sshd\_config has the following setting \(and reload: service ssh reload\)

```text
AllowTcpForwarding yes
```

### Configuration

Next, create a `main.tf` file within your local `gradient-cluster` directory that you created; `main.tf` will be a sibling file to the `backend.tf` file that you may have created already. Note: this file _must_ be named `main.tf` since Terraform looks for this configuration file by name.

In `main.tf`, copy and paste the Terraform configuration below \(note the copy icon in the upper right corner\). Be sure to follow the value replacement instructions further below, as well.

#### SSL Configuration

The Gradient installer can use Let's Encrypt to create a SSL certificate, verify it by making entries with your DNS provider, and install the certificate on your cluster to secure access to notebooks, model deployments, etc. For this to work, your domains DNS provider must be [on the supported list](../lets-encrypt-dns-providers.md). To use this functionality, create a block in your `main.tf` file similar to the one in the example below. Use the `letsencrypt_dns_name` that matches your provider in the list, and provide the required authentication field\(s\) as specified in the `letsencrypt_dns_settings` column.

If you don't want to use automatic SSL, use `tls_cert` and `tls_key` entries and be sure the SSL certificate files are located in the directory and filenames specified \(or change them in the `main.tf` file\).

You can use either the Let's Encrypt block OR the manual certificate block, but not both.

```text
module "gradient_metal" {
    source = "../gradient-installer/gradient-metal"

    // name should only have letters, numbers, and dashes
    name = "cluster-name"
    artifacts_access_key_id = "artifacts-access-key-id"
    artifacts_path = "s3://artifacts-bucket"
    artifacts_secret_access_key = "artifacts-secret-access-key"

    cluster_apikey = "cluster-apikey-from-paperspace-com"
    cluster_handle = "cluster-handle-from-paperspace-com"
    domain = "gradient.mycompany.com"
    cpu_selector = "dgx.gpu"
    gpu_selector = "dgx.gpu"

    k8s_master_node = {
        ip = "master_node_ip1"
        pool-type = "gpu"
        pool-name = "dgx.gpu"
    }
    
    k8s_workers = []
    /*
    // For multiple nodes
    k8s_workers = [
        {
            ip = "worker_ip1"
            pool-type = "gpu"
            pool-name = "dgx.gpu"
        },
        {
            ip = "worker_ip2"
            pool-type = "gpu"
            pool-name = "dgx.gpu"
        }
    ]*/

    shared_storage_path = "/srv/gradient"
    shared_storage_server = "shared-nfs-storage.com"
    ssh_key_path = "./gradient_rsa"
    ssh_user = "ubuntu"

    // insert a SSL block below - the first example is for Cloudflare DNS

    /*
    // Example using cloudflare, check docs for list of supported DNS providers
    letsencrypt_dns_name = "cloudflare"
    letsencrypt_dns_settings = {
        CF_API_KEY = "[Global cloudflare key]"
        CF_API_EMAIL = "[Cloudflare email address]"
    }
    */
    
    // or disable automatic SSL by specifying cert files below
    // tls_cert = file("./ssl-bundle.crt")
    // tls_key = file("./ssl.key")
}
```

Replace the following fields with the appropriate values:

* `name` \(the same name used when registering the new cluster in the Paperspace web console\)
* `artifacts_access_key_id` \(the key for the bucket that was set up for artifacts storage\)
* `artifacts_path` \(the full s3 path to the bucket\)
* `artifacts_secret_access_key`
* `cluster_apikey` \(provided during registration of the new cluster\)
* `cluster_handle` \(provided during registration of the new cluster\)
* `cpu_selector` \(node selector to run CPU workloads, defaults to "metal-cpu"\)
* `domain` \(same as what was entered during cluster registration\)
* `gpu_selector` \(node selector to run GPU workloads, defaults to "metal-gpu"\)
* `master_ip1, worker_ip1, worker_ip2` \(see below for IP networking info\)
* `shared_storage_path` and `shared_storage_server` \(see below for NFS info\)
* `ssh_key_path` \(for the key generated above\)
* `ssh_user` \(a ssh user who has the above public key in its authorized\_keys file\)
* _Also_, either use automatic SSL or be sure the SSL certificate files are located in your gradient-cluster directory, and replace the filenames in your `main.tf` configuration to match them as needed.

#### IP networking

Each node should have an IP address that's accessible from the computer where the Gradient installer is being run. There must be one master node and at least two workers. All worker nodes must be able to access the master node, and the master node must be accessible from the internet.

All nodes must be able to access various hosts on the internet, including Paperspace's hub sites, logging sites, and Docker Hub.

#### NFS setup

Gradient installer requires a NFS host for runtime file storage. This server should have a high-bandwidth, low-latency connection from the cluster – ideally within the same datacenter or cloud region. 

#### Installation

Next, install and configure the nodes using Docker and Terraform:

```text
docker run -ti --rm -v $(pwd)/gradient-cluster:/home/paperspace/gradient-cluster nvcr.io/partners/gradient:0.1.22
```

Gradient requires two DNS CNAME records to make external services accessible. Use the IP address of the master node as the target for these records, as shown below.

Example:

`*.gradient.mycompany.com [master node ip address]`

`gradient.mycompany.com [master node ip address]`

#### Managing the Kubernetes cluster with KUBECONFIG

For those familiar with Kubernetes, a file will be generated in the gradient-cluster folder that contains the Kubernetes `kubeconfig`. To use the generated KUBECONFIG, the computer running kubectl will need to have access to the cluster's master node.

Managing the Kubernetes cluster manually is not required to use Gradient.

#### Updating the Gradient cluster

Run this command to update Gradient to the latest version:

```text
docker run -ti --rm -v $(pwd)/gradient-cluster:/home/paperspace/gradient-cluster nvcr.io/partners/gradient:0.1.22
```

#### Uninstalling Gradient

Run this command to uninstall Gradient:

```text
docker run -ti --rm -v $(pwd)/gradient-cluster:/home/paperspace/gradient-cluster nvcr.io/partners/gradient:0.1.22 terraform destroy
```

