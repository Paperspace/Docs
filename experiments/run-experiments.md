# Run Experiments from the CLI

Gradient supports [GitHub-integrated projects](../projects/gradientci.md) and standalone projects. In a standalone project, you can use the GUI experiment builder directly in the application, or the CLI, which enables you to run experiments manually and programmatically from your command line for maximum flexibility.

## How to run a single-node or multinode experiment

Use the `--help` flag to bring up information in your terminal.

```bash
$ paperspace-python experiments create singlenode --help
Usage: paperspace-python experiments create singlenode [OPTIONS]

$ paperspace-python experiments create multinode --help
Usage: paperspace-python experiments create multinode [OPTIONS]
```

### Creating a singlenode experiment using the CLI

The following command creates and starts a singlenode experiment called `singleEx` and places it within the Gradient Project identified by the `--projectId` option.  \(Note: in some early versions of the CLI this option was called `--projectHandle`.\)

```bash
paperspace-python experiments createAndStart singlenode \
  --projectId <your project id> \
  --name singleEx \
  --experimentEnv "{\"EPOCHS_EVAL\":5,\"TRAIN_EPOCHS\":10,\"MAX_STEPS\":1000,\"EVAL_SECS\":10}" \
  --container tensorflow/tensorflow:1.13.1-gpu-py3 \
  --machineType K80 \
  --command "python mnist.py" \
  --workspaceUrl https://github.com/Paperspace/mnist-sample.git \
  --modelType Tensorflow \
  --modelPath /artifacts
```

To run this command substitute an existing project ID for &lt;your project id&gt;.  You can get an existing project id by going to [your projects list](https://www.paperspace.com/console/projects) and creating a new project or opening an existing project and copying the Project ID value.  You can also get a list of existing projects and their IDs from the command line using the command `paperspace-python projects list`.

For more information about this sample experiment see the README in the mnist-sample github repo: [https://github.com/Paperspace/mnist-sample](https://github.com/Paperspace/mnist-sample). \(Note: the code for this experiment can be run in both singlenode and multinode training modes.\)

### Creating a multinode experiment using the CLI

The following command creates and starts a multinode experiment called `multiEx` and places it within the Gradient Project identified by the `--projectId` option.  \(Note: in some early versions of the CLI this option was called `--projectHandle`.\)

```bash
paperspace-python experiments createAndStart multinode \
  --name multiEx \
  --projectId <your project id> \
  --experimentTypeId GRPC \ 
  --workerContainer tensorflow/tensorflow:1.13.1-gpu-py3 \
  --workerMachineType K80 \
  --workerCommand "python mnist.py" \
  --workerCount 2 \
  --parameterServerContainer tensorflow/tensorflow:1.13.1-gpu-py3 \
  --parameterServerMachineType K80 \
  --parameterServerCommand "python mnist.py" \
  --parameterServerCount 1 \
  --workspaceUrl https://github.com/Paperspace/multinode-mnist.git \
  --modelType Tensorflow
```

To run this command substitute an existing project ID for &lt;your project id&gt;.  You can get an existing project id by going to [your projects list](https://www.paperspace.com/console/projects) and creating a new project or opening an existing project and copying the Project ID value.  You can also get a list of existing projects and their IDs from the command line using the command `paperspace-python projects list`.

The command above specifies the use of the gRPC framework and names the same Docker container, machine type, and programmatic command for both the 2 workers and the 1 parameter server.

Finally, the command specifies the workspace to pull the Python script from as a public GitHub repository.

For more information about this sample experiment see the README in the mnist-sample github repo: [https://github.com/Paperspace/mnist-sample](https://github.com/Paperspace/mnist-sample). \(Note: the code for this experiment can be run in both singlenode and multinode training modes.\)

## Options common to both singlenode and multinode experiments

```text
  --name TEXT                  Name of new experiment  [required]
  --ports TEXT                 Port to use in new experiment
  --workspace TEXT             Path to workspace directory
  --workspaceArchive TEXT      Path to workspace .zip archive
  --workspaceUrl TEXT          Project git repository url
  --workingDirectory TEXT      Working directory for the experiment
  --artifactDirectory TEXT     Artifacts directory
  --clusterId TEXT             Cluster ID
  --experimentEnv JSON_STRING  Environment variables in a JSON
  --projectId TEXT             Project ID  [required]
  --modelType TEXT             Model type
  --modelPath TEXT             Model path
  --apiKey TEXT                API key to use this time only
  --help                       Show this message and exit
```

## Options specific to singlenode experiments

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

Also, using the `--containerUser` option, you can specify a UNIX user name to be used as the UNIX identity for running the specified command in the container.  If no containerUser  is specified, the user will default to 'root' in the container.  This is useful when running a public container image with a different expected user, or when building a container image from a Dockerfile.

## Options specific to multinode experiments

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

In the case of multinode experiments, both worker and parameter server instances need a container, machine type, command, count, and optionally a Docker registry username and password.

Note: `--containerUser` is not a supported option for multinode experiments currently.

