# Containers: Public & Private

## About

When you run a Gradient Experiment you must provide a docker container within which your code will execute. 

There are two types of containers you can provide: **public** or **private**

## Public Containers

The CLI expects that you provide a container using the standard Docker syntax. For example, any container on the Docker Hub registry will work out of the box. To pull the official Tensorflow container, you would check here: [https://hub.docker.com/r/tensorflow/tensorflow/](https://hub.docker.com/r/tensorflow/tensorflow/)

And your container would take the form:

tensorflow/tensorflow:1.5.1-gpu where 1.5.1-gpu is the "tag" taken from here: [https://hub.docker.com/r/tensorflow/tensorflow/tags/](https://hub.docker.com/r/tensorflow/tensorflow/tags/)

Example use:

```text
gradient experiments run ... --container tensorflow/tensorflow:1.5.1-gpu
```

## Private Containers

If you specify a container that is hosted on a private registry, then you will need to authenticate using the optional experiment parameters: _registryUsername_ and _registryPassword_.

Here are some details on the pulling from private docker repositories:

There are two new options on the `gradient experiments run` and `gradient experiments create`methods to be used when specifying a container \(aka a docker image\) from a private docker repository: `--registryUsername` and `--registryPassword`.

Example use:

```text
gradient experiments run ...  --container "docker.io:/paperspace/tom_test_private" --registryUsername "tompaperspace" --registryPassword "xxxxxxxx"
```

_Notes:_ You need to specify the username and password each time you reference a private docker repository in an experiment submission. The credentials are transmitted over ssl and cached for the lifetime of the experiment. If you clone the experiment the credentials are automatically reused.

The credential options `--registryUsername` and `--registryPassword` should be sufficient for a number of private docker registry services, including

* Docker Hub
* Amazon EC2 Container Registry
* Google Container Registry
* JFrog/Bintray.io
* Quay.io
* Custom registries running Docker Registry v2 protocol, as long as they are publicly accessible on the internet.

The form of the repository link, and the format of the username and password are specific for some of these registries, but are publicly documented. The following provides a summary for Docker Hub, AWS and GCP:

#### 1. Docker Hub

Username: &lt;your Docker ID&gt;  
Password: &lt;your Docker ID password&gt;

Container link format: "docker.io/&lt;organization-or-username&gt;/&lt;repository-name&gt;\[:&lt;tag&gt;\]"

Example:

```text
paperspace jobs create ... --container "docker.io/myorganization/my_private_repo:latest" \
--registryUsername "myusername" --registryPassword "mypassword"
```

####  2. Amazon Elastic Container Service

Username: "AWS"  
Password: &lt;value of '-p' option from output of the AWS SDK command "aws ecr get-login --no-include-email"&gt;

Container link format: "&lt;aws\_account\_id&gt;.dkr.ecr.us-east-1.amazonaws.com/\[&lt;namespace&gt;/\]&lt;repository-name&gt;"  
  
Example:

Install and configure the AWS SDK on your local computer, then execute:

```text
aws ecr get-login --no-include-email
```

\(Note: if the --no-include-email is reported as not supported, you may need to update your aws cli using pip3.\)

It will produce output similar to the following:

```text
"docker login -u AWS -p sb2FkIjSIsImV4calksdhwTTyslia189231qwdgqer3kIjSIsImV4calksd123eiadfviuaigq2 \
9438hvehraw8437rgfq4398yq934ghalibrla478tqkIjSIsImV4calksd34ariIsImV4calksdhliarhg9q34yt9huargq934t \
123jAUhi37rgfq4398yq934ghalibrla478tq348437rgfqIsImV4calkIjSIsImV4calksdksdhlia4398yq934ghlibrla478 \
brla478tq348437rgfqIsImV123jAUhi37rgfq4398yq9sImV4calksdksghlib34ghali4calkIjSIrla478dhlia4398yq934 \
q34t843q98iOjE1MTYyNjUx https://XXXXXXXXXXXX.dkr.ecr.us-east-1.amazonaws.com"
```

Use the value of the '-p' option from the actual output as the password value in the `gradient experiments` method.  
\(note: the value may span multiple lines\):

```text
gradient experiments run ... --container "XXXXXXXXXXXX.dkr.ecr.us-east-1.amazonaws.com/mynamespace/tom_test_private" \
--registryUsername "AWS" --registryPassword sb2FkIjSIsImV4calksdhwTTyslia189231qwdgqer3kIjSIsImV4calksd123eiadfviuaigq2 \
9438hvehraw8437rgfq4398yq934ghalibrla478tqkIjSIsImV4calksd34ariIsImV4calksdhliarhg9q34yt9huargq934t \
123jAUhi37rgfq4398yq934ghalibrla478tq348437rgfqIsImV4calkIjSIsImV4calksdksdhlia4398yq934ghlibrla478 \
brla478tq348437rgfqIsImV123jAUhi37rgfq4398yq9sImV4calksdksghlib34ghali4calkIjSIrla478dhlia4398yq934 \
q34t843q98iOjE1MTYyNjUx
```

For more details and options see: [https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html)

####  3. Google Container Registry

Username: "\_json\_key"  
Password: &lt;service account JSON Keyfile contents&gt;

Container link format: "\[us.\|eu.\|asia.\]gcr.io/&lt;project-id&gt;/&lt;repository-name&gt;\[:&lt;tag&gt;\]"

Example:

To get this create a service account JSON key file for your project, following these instructions:  
[https://support.google.com/cloud/answer/6158849\#serviceaccounts](https://support.google.com/cloud/answer/6158849#serviceaccounts)  
  
Once you have downloaded your JSON key file, rename it to "keyfile.json".

Use the contents of the keyfile as the password value in the Gradient experiments method:

```text
gradient jobs create ... --container "gcr.io/myproject/my_private_repo:latest" \
--registryUsername "_json_key" --registryPassword "$(cat keyfile.json)"
```

Note: do not base64 encode the contents of the keyfile. It will be encoded by the gradient job runner at runtime.

For more details and other options see: [https://cloud.google.com/container-registry/docs/advanced-authentication](https://cloud.google.com/container-registry/docs/advanced-authentication)

### Other Considerations

If you are running on a GPU-node your container will need to include the relevant NVIDIA GPU drivers. This can be done most easily by basing your container off of the official NVIDIA docker containers. i.e. the top line of your Dockerfile would be:

```text
FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu14.04
Checkout the NVIDIA/Cuda repo for more possible tags: https://hub.docker.com/r/nvidia/cuda/tags/
```

