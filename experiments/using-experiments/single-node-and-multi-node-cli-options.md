# Single-node & multi-node CLI options

### Options common to both single-node and multi-node experiments

```text
  --name TEXT                  Name of new experiment  [required]
  --ports TEXT                 Port to use in new experiment
  --workspace TEXT             Path to workspace directory
  --workspaceArchive TEXT      Path to workspace .zip archive
  --workspaceUrl TEXT          Project git repository url
  --workspaceUsername          Github username for private repo
  --workspacePassword          Github password for private repo
  --workspacePassword wd3gG9WyReTWbMpmkKTFJ \
  --workingDirectory TEXT      Working directory for the experiment
  --artifactDirectory TEXT     Artifacts directory
  --clusterId TEXT             Cluster ID
  --experimentEnv JSON_STRING  Environment variables in a JSON
  --projectId TEXT             Project ID  [required]
  --modelType TEXT             Model type
  --modelPath TEXT             Model path
```

{% hint style="info" %}
`workspaceArchive` and `workspaceUrl` are deprecated as of the 0.6.0 release version of the CLI. You can just use workspace going forward!

For `workspace`, valid schemes for values specifying a remote URL are: `https`, `git+https`, and `s3`, or you can specify `"none"`. This means that, for example, git@github is _not_ a valid scheme for a workspace.
{% endhint %}

### Options specific to single-node experiments

```text
  --container TEXT             Container  [required]
  --machineType TEXT           Machine type  [required]
  --command TEXT               Container entrypoint command  [required]
  --containerUser TEXT         Container user
  --registryUsername TEXT      Registry username
  --registryPassword TEXT      Registry password
```

A container, machine type, and command are required.

Optionally a Docker registry username and password can be provided for accessing private docker registry container images via the `--registryUsername` and `--registryPassword` options.

Also, using the `--containerUser` option, you can specify a UNIX user name to be used as the UNIX identity for running the specified command in the container. If no containerUser is specified, the user will default to 'root' in the container. This is useful when running a public container image with a different expected user, or when building a container image from a Dockerfile.

### Options specific to multi-node experiments

```text
  --experimentTypeId [GRPC|MPI]   Experiment Type ID  [required]
  --workerContainer TEXT          Worker container  [required]
  --workerMachineType TEXT        Worker machine type  [required]
  --workerCommand TEXT            Worker command  [required]
  --workerCount INTEGER           Worker count  [required]
  --parameterServerContainer TEXT
                                  Parameter server container  [required]
  --parameterServerMachineType TEXT
                                  Parameter server machine type  [required]
  --parameterServerCommand TEXT   Parameter server command  [required]
  --parameterServerCount INTEGER  Parameter server count  [required]
  --workerContainerUser TEXT      Worker container user
  --workerRegistryUsername TEXT   Worker container registry username
  --workerRegistryPassword TEXT   Worker registry password
  --parameterServerContainerUser TEXT
                                  Parameter server container user
  --parameterServerRegistryContainerUser TEXT
                                  Parameter server registry container user
  --parameterServerRegistryPassword TEXT
                                  Parameter server registry password
```

In the case of multi-node experiments, both worker and parameter server instances need a container, machine type, command, count, and optionally a Docker registry username and password.

Note: `--containerUser` is not a supported option for multi-node experiments currently.

