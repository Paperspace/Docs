# Building Docker Containers with Jobs

Gradient containers can be created from a Dockerfile. Three options are available:

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

