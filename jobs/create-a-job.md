# Create a Job

## About

Create a new Paperspace job, and tail its log output.

{% hint style="info" %}
**Note:** if a project is not defined for the current working directory, and you are running in command line mode, a project configuration settings file will be created. Use`--init false` or specify`--project [projectname]`to override this behavior.
{% endhint %}

## Syntax

```text
$ gradient jobs create <namespace> <command> [options...]
```

### Job Parameters Basics

* Machine Type: Such as `--P100` or `--C7` or `--TPU`
* Container: Such as `--tensorflow/tensorflow:1.5.1-gpu`
* Command: Such as `"./do.sh"`

## Example Use

```text
$ gradient jobs create \
    --container "http://dockerhub.com/mycontainer" \
    --machineType "P5000" \
    --command "/paperspace/run.sh"
```

## Job Parameters Complete List

**Properties**

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |


| `container` | string | &lt;optional&gt; | A reference to a docker image in a public or private docker registry, or a container name provided by Paperspace. Docker image repository references must be in lowercase and may include a tag and a hostname prefix followed by a slash; if committed the hostname defaults to that of the public Docker Hub registry. An example docker image reference: `docker.io/mynamespace/myimage:mytag`. A container name may be mixed case. \(Designated container names are currently only provided as part of various Gradient tutorials and samples.\) |
| :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>machineType</code>
      </th>
      <th style="text-align:left">string</th>
      <th style="text-align:left">&lt;optional&gt;
        <br />
      </th>
      <th style="text-align:left">
        <p>An optional machine type to run the job on: either &apos;GPU+&apos;, &apos;P4000&apos;,
          &apos;P5000&apos;, &apos;P6000&apos;, &apos;V100&apos;, &apos;K80&apos;,
          &apos;P100&apos;, or &apos;TPU&apos;.</p>
        <p>Defaults to &apos;K80&apos;.</p>
        <p>Note: the &apos;K80&apos;, &apos;P100&apos;, and &apos;TPU&apos; machineTypes
          run on Google Cloud Platform (GCP). The other machineTypes run on the Paperspace
          Cloud. Google Cloud platform and Paperspace Cloud have distinct Job Storage
          spaces; Job storage is not currently shared between these two cloud environments.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| `name` | string | &lt;optional&gt; | An optional name or description for this job. If committed, the job name defaults to 'job N' where N represents the Nth job instance for the given project. |
| :--- | :--- | :--- | :--- |


| `project` | string | &lt;optional&gt; | The name of the project for this job. If not provided, this is taken from the .ps\_project/config.json file, or the current directory name. |
| :--- | :--- | :--- | :--- |


| `projectId` | string | &lt;optional&gt;  | The project id of an existing project for this job. Note: if projectId is specified, the project parameter cannot be specified. |
| :--- | :--- | :--- | :--- |


| `command` | string | &lt;optional&gt; | An optional command to run within the workspace or container. |
| :--- | :--- | :--- | :--- |


| `workspace` | string | &lt;optional&gt; | An optional path to a workspace, or link to a git repository to upload and merge with the container. If a zip file name is provided it is uploaded instead. If no workspace is provided the current directory is zipped up and transferred. If the workspace is 'none', no workspace is merged and the container is run as-is. To download a git repository provide an https repository link and optionally prefix it with 'git+', e.g. 'https://github.com/MyProjects/MyRepo.git'. If the 'git+' prefix is not specified, it is added at the time of download to the job runner machine. S3 links are also supported using the schema 's3://bucketname/objectname'. |
| :--- | :--- | :--- | :--- |


| `dataset` | string | &lt;optional&gt; | An optional reference to a dataset to be merged with the container. |
| :--- | :--- | :--- | :--- |


| `registryUsername` | string | &lt;optional&gt; | An optional username for accessing an image hosted on a private container registry. Note: you must specify this option every time a private image is specified for the container. |
| :--- | :--- | :--- | :--- |


| `registryPassword` | string | &lt;optional&gt; | An optional password for accessing an image hosted on a private container registry. Note: you must specify this option every time a private image is specified for the container. |
| :--- | :--- | :--- | :--- |


| `workspaceUsername` | string | &lt;optional&gt; | An optional username for accessing a private git repository. Note: you must specify this option every time a private git repository is specified for the workspace. |
| :--- | :--- | :--- | :--- |


| `workspacePassword` | string | &lt;optional&gt; | An optional password for accessing a private git repository. We recommend using an OAuth token \(GitHub instructions can be found [here](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)\). Note: you must specify this option every time a private git repository is specified for the workspace. |
| :--- | :--- | :--- | :--- |


| `ports` | string | &lt;optional&gt; | An optional list of port mappings to open on the job cluster machine while the job is running. The port mappings are specified as 'XXXX:YYYY' where XXXX is an external port number and YYYY is an internal port number. Multiple port mappings can be provided as a comma separated list. Port numbers must be greater than 1023. Note: only /tcp protocol usage is supported. |
| :--- | :--- | :--- | :--- |


| `tail` | boolean | &lt;optional&gt; | Optional; defaults to true in command line mode only. Specify false to disable automatic tailing. |
| :--- | :--- | :--- | :--- |


| `json` | boolean | &lt;optional&gt; | Optional; if true, do not write progress to standard out. `--json`with no value is equivalent to true. |
| :--- | :--- | :--- | :--- |


{% hint style="info" %}
Environmental variables are available for use within the context of your job. The following host config options are currently exposed within the container:

`$PS_HOST_PUBLIC_IP_ADDRESS` - the public IP address of the host machine running the job

`$PS_HOST_PRIVATE_IP_ADDRESS` - the private IP address of the host machine running the job

`$PS_HOSTNAME` - the hostname of the host machine running the job

These can be used in conjunction with the `ports` option to send HTTP traffic to the job while it's in progress for example.
{% endhint %}

### New: Run jobs from Dockerfiles

Gradient job containers can now be created from a Dockerfile. Three options are available:

1\) The job can build the container image and push it to a remote registry only. This is useful in cases where you want access to a GPU to build a GPU-enabled container but do not have one on-hand.

2\) The job can build the container image and run commands against a running instance of the container without uploading to a remote registry. Useful for experimenting with gradient jobs defined by Dockerfiles and cases where you are only interested in the results of the job.

3\) The job can build the container image, upload the image to a remote registry, and then run commands against a running instance of the container . Useful for building images and experimenting with gradient jobs defined by Dockerfiles while retaining the original image used.

The following new job fields are available:

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `useDockerfile` | boolean | &lt;optional&gt; | determines whether to build from Dockerfile \(default false\). Do not include a --container argument when using this flag. |
| `buildOnly` | boolean | &lt;optional&gt; | determines whether to only build and not run image \(default false\) |
| `registryTarget` | string | &lt;optional&gt; | registry location to push image to |
| `registryTargetUsername` | string | &lt;optional&gt; | registry username |
| `registryTargetPassword` | string | &lt;optional&gt; | registry password |
| `relDockerfilePath` | string | &lt;optional&gt; | relative location of dockerfile in workspace \(default "./Dockerfile"\) |

For example, to run a job that only builds a container image and pushes to a remote registry:

```text
gradient jobs create --apiKey XXXXXXXXXXXXXXXXX --workspace https://github.com/ianmiell/simple-dockerfile --useDockerfile true --buildOnly true  --registryTarget my-registry/image:0.1-test --registryTargetUsername myusername --registryTargetPassword 123456
```

Note that if you selected `buildOnly` you should supply always a registry target and credentials.

To run a job that builds a container image, pushes to a remote registry, and then runs a command inside an instance of the running container:

```text
gradient jobs create --apiKey XXXXXXXXXXXXXXXXX --workspace https://github.com/ianmiell/simple-dockerfile --useDockerfile true --buildOnly false --command "echo hello"  --registryTarget my-registry/image:0.1-test --registryTargetUsername myusername --registryTargetPassword 123456
```

To run a job that builds the container image and then runs an instace of the container, without pushing to a remote registry:

```text
gradient jobs create --apiKey XXXXXXXXXXXXXXXXX --workspace https://github.com/ianmiell/simple-dockerfile --useDockerfile true --buildOnly false --command "echo hello"
```

{% hint style="info" %}
Note: commands run during the build step from the Dockerfile, like CMD \["command", "arg1"...\] are run inside the image layers as it's being built. Once the container image is ready to run the --command argument is used to determine what command to run against the built image.
{% endhint %}

