# Install on NVIDIA DGX

This version should be used for NVIDIA DGX-1 hosts. Terraform, running inside a Docker container, will be used to provision a Kubernetes cluster on the hosts and will require ssh access to all hosts in order to connect. Note that in this scenario auto-scaling is not available – all nodes will be running at all times.

Be sure to follow the [pre-installation steps](pre-installation-steps.md), and then run this:

```text
mkdir gradient-cluster
ssh-keygen -f gradient-cluster/gradient_rsa
```

#### Requirements

On the computer where you plan to run the Gradient installer, you must have Docker installed with a user that has access to /var/run/docker.sock.

For the NVIDIA DGX-1 hosts:

* Ubuntu 18.04
* NFS server available to all nodes
* Docker installed on all hosts \(or use `"setup_docker = true"` in the main.tf file to have Docker installed by Terraform\)
* Set default docker runtime to nvidia in /etc/docker/daemon.json \(or just set `"setup_nvidia = true"` in the main.tf file, below\) 

```text
The following is an example of how the added line appears in the JSON file. Do not remove any pre-existing content when making this change.
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

* Ensure your SSH user has access to the docker group in /etc/group:

```text
docker:x:999:ubuntu
```

* Ensure your SSH public key is installed on each host
* Ensure sudo is enabled for the account you're logging into
* Ensure /etc/sshd/sshd\_config has the following setting \(and reload: service ssh reload\)

```text
AllowTcpForwarding yes
```

#### Configuration

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
* master\_ip1, worker\_ip1, worker\_ip2 \(see below for IP networking info\)
* shared\_storage\_path and shared\_storage\_server \(see below for NFS info\)
* ssh\_key\_path \(for the key whose public key is on the nodes being configured\)
* ssh\_user \(a ssh user who has the above public key in its authorized\_keys file\)

Also be sure the SSL certificate files are located in the directory and filenames specified \(or change them in your main.tf file\).

```text
module "gradient_metal" {
    source = "../gradient-terraform/gradient-metal"

    // name should only have letters, numbers, and dashes
    name = "cluster-name"
    artifacts_access_key_id = "artifacts-access-key-id"
    artifacts_path = "s3://artifacts-bucket"
    artifacts_secret_access_key = "artifacts-secret-access-key"

    cluster_apikey = "cluster-apikey-from-paperspace-com"
    cluster_handle = "cluster-handle-from-paperspace-com"
    domain = "gradient.mycompany.com"
    global_selector = "dgx.gpu"

    k8s_master_ips = [
        "master_ip1",
    ]
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
    ssh_key_path = "~/gradient_rsa"
    ssh_user = "ubuntu"

    tls_cert = replace(file("./ssl-bundle.crt"), "\n", "\\n")
    tls_key = replace(file("./ssl.key"), "\n", "\\n")
}
```

#### IP networking

Each node should have an IP address that's accessible from the computer where the Gradient installer is being run. There must be one master node and at least two workers. All worker nodes must be able to access the master node, and the master node must be accessible from the internet.

All nodes must be able to access various hosts on the internet, including Paperspace's hub sites, logging sites, and Docker Hub.

#### NFS setup

Gradient installer requires a NFS host for runtime file storage. This server should have a high-bandwidth, low-latency connection from the cluster – ideally within the same datacenter or cloud region. 

#### Installation

Next, install and configure the nodes using Docker and Terraform:

```text
docker run -ti --rm -v $(pwd)/gradient-cluster:/home/paperspace/gradient-cluster paperspace/gradient-terraform
```

Gradient requires two DNS CNAME records to make external services accessible. Use the IP address of the master node as the target for these records, as shown below.

Example:

`*.gradient.mycompany.com [master node ip address]`

`gradient.mycompany.com [master node ip address]`

#### Managing the Kubernetes cluster with KUBECONFIG

For those familiar with Kubernetes, a file will be generated in the gradient-cluster folder that contains the Kubernetes `kubeconfig`. To use the generated KUBECONFIG, the computer running kubectl will need to have access to the cluster's master node.

Managing the Kubernetes cluster manually is not required to use Gradient.

#### Updating the Gradient cluster



#### Uninstalling Gradient

Run this command to uninstall Gradient:

```text
docker run -ti --rm -v $(pwd)/gradient-cluster:/home/paperspace/gradient-cluster paperspace/gradient-terraform terraform destroy
```

