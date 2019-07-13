# Create a Job

## About

Create a new Paperspace job

{% hint style="info" %}
**Note:** if a project is not defined for the current working directory, and you are running in command line mode, a project configuration settings file will be created. Use`--init false` or specify`--project <your-project-name>`to override this behavior.
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
    --name "my job" \
    --container "http://dockerhub.com/mycontainer" \
    --machineType "P5000" \
    --command "/paperspace/run.sh"
```

## Job Parameters Complete List

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>name</code>
      </td>
      <td style="text-align:left">[required]</td>
      <td style="text-align:left">Job name</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>machineType</code>
      </td>
      <td style="text-align:left">K80</td>
      <td style="text-align:left">An optional machine type to run the job on: either &apos;GPU+&apos;, &apos;P4000&apos;,
        &apos;P5000&apos;, &apos;P6000&apos;, &apos;V100&apos;, &apos;K80&apos;,
        &apos;P100&apos;, or &apos;TPU&apos;.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>container</code>
      </td>
      <td style="text-align:left">paperspace/tensorflow-python</td>
      <td style="text-align:left">A reference to a docker image in a public or private docker registry,
        or a container name provided by Paperspace. Docker image repository references
        must be in lowercase and may include a tag and a hostname prefix followed
        by a slash; if committed the hostname defaults to that of the public Docker
        Hub registry. An example docker image reference: docker.io/mynamespace/myimage:mytag.
        A container name may be mixed case. (Designated container names are currently
        only provided as part of various Gradient tutorials and samples.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>command</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Job command/entrypoint</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ports</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An optional list of port mappings to open on the job cluster machine while
        the job is running. The port mappings are specified as &apos;XXXX:YYYY&apos;
        where XXXX is an external port number and YYYY is an internal port number.
        Multiple port mappings can be provided as a comma separated list. Port
        numbers must be greater than 1023. Note: only /tcp protocol usage is supported.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspace</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Path to workspace directory. (Soon also will support a path to a workspace
        archive or git repository URL.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceArchive</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Path to workspace archive. (Currently being deprecated in an upcoming
        version.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceUrl</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Project git repository URL. (Currently being deprecated in an upcoming
        version.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workingDirectory</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Working directory for the experiment</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>experimentId</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Experiment Id</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>jobEnv</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Environmental variables in JSON String Format. Example:</p>
        <p>{ &quot;HKS_EPOCHS&quot;: 1, &quot;HKS_MAX_EVALS&quot;: 4, &quot;DATASET_SIZE&quot;:
          10000 }</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>project</code>
      </td>
      <td style="text-align:left">$CWD</td>
      <td style="text-align:left">The name of the project for this job. If not provided, this is taken from
        the .ps_project/config.json file, or the current directory name.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>projectID</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Project ID</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>apiKey</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">API key to use this time only</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ignoreFiles</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Ignore certain files from uploading</td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
Environment variables are available for use within the context of your job. The following host config options are currently exposed within the container:

`$PS_HOST_PUBLIC_IP_ADDRESS` - the public IP address of the host machine running the job

`$PS_HOST_PRIVATE_IP_ADDRESS` - the private IP address of the host machine running the job

`$PS_HOSTNAME` - the hostname of the host machine running the job

These can be used in conjunction with the `ports` option to send HTTP traffic to the job while it's in progress for example.
{% endhint %}

### Run jobs from Dockerfiles

_Note: to run jobs from Dockerfiles, use_ [_paperspace-node_](https://github.com/Paperspace/paperspace-node)_, or gradient-cli._

Gradient job containers can be created from a Dockerfile. Three options are available:

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
gradient jobs create --apiKey XXXXXXXXXXXX --workspace https://github.com/ianmiell/simple-dockerfile --useDockerfile true --buildOnly true  --registryTarget my-registry/image:0.1-test --registryTargetUsername myusername --registryTargetPassword 123456
```

Note that if you selected `buildOnly` you should supply always a registry target and credentials.

To run a job that builds a container image, pushes to a remote registry, and then runs a command inside an instance of the running container:

```text
gradient jobs create --apiKey XXXXXXXXXXXX --workspace https://github.com/ianmiell/simple-dockerfile --useDockerfile true --buildOnly false --command "echo hello"  --registryTarget my-registry/image:0.1-test --registryTargetUsername myusername --registryTargetPassword 123456
```

To run a job that builds the container image and then runs an instance of the container, without pushing to a remote registry:

```text
gradient jobs create --apiKey XXXXXXXXXXXX --workspace https://github.com/ianmiell/simple-dockerfile --useDockerfile true --buildOnly false --command "echo hello"
```

{% hint style="info" %}
Note: commands run during the build step from the Dockerfile, like CMD \["command", "arg1"...\] are run inside the image layers as it's being built. Once the container image is ready to run, the `--command` argument is used to determine what command to run against the built image.
{% endhint %}

