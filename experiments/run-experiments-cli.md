# Run Experiments via the CLI

The Gradient CLI enables you to run experiments manually and programmatically from your command line for maximum flexibility.  Once you have the [CLI installed](../get-started/install-the-cli.md), use the alias `gradient` plus any further commands you wish to run.

Note that you can use the `--help` option at any time to reveal information in your terminal about the current command you wish to use. Alternately, if you simply try to run a command, the CLI will prompt you for additional subcommands that you may be intending to use, as well as required options that are missing from your command.

```bash
Usage: gradient [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  apiKey           Save your api key
  deployments      Manage deployments
  experiments      Manage experiments
  hyperparameters  Manage hyperparameters
  jobs             Manage gradient jobs
  logout           Log out / remove apiKey from config file
  machines         Manage machines
  models           Manage models
  projects         Manage projects
  run              Run script or command on remote cluster
  version          Show the version and exit
```

## Running experiments

For programmatic use of the CLI, there is the `create` command, which simply creates an experiment in a target project, with the specified options.

Alternately, for more interactive use of the CLI, there is `run`, which allows you to both create and automatically start an experiment with one command. With this command, logs will automatically stream once the experiment has been created and started.

There are separate subcommands `singlenode` and `multinode` experiments.

```bash
gradient experiments run singlenode --help
Usage: gradient experiments create singlenode [OPTIONS]

gradient experiments run multinode --help
Usage: gradient experiments create multinode [OPTIONS]
```

### Creating a single-node experiment using the CLI

The following command creates and starts a single-node experiment called `singleEx` and places it within the Gradient Project identified by the `--projectId` option. 

```bash
gradient experiments run singlenode \
  --projectId <your-project-id> \
  --name singleEx \
  --experimentEnv "{\"EPOCHS_EVAL\":5,\"TRAIN_EPOCHS\":10,\"MAX_STEPS\":1000,\"EVAL_SECS\":10}" \
  --container tensorflow/tensorflow:1.13.1-gpu-py3 \
  --machineType K80 \
  --command "python mnist.py" \
  --workspaceUrl https://github.com/Paperspace/mnist-sample.git \
  --modelType Tensorflow \
  --modelPath /artifacts
```

{% hint style="info" %}
See more info about [model paths](../models/model-path.md#default-paths) and their default values, including for if you want to deploy your models via Gradient Deployments.
{% endhint %}

To run this command substitute an existing project ID for &lt;your-project-id&gt;. You can get an existing project id by going to [your projects list](https://www.paperspace.com/console/projects) and creating a new project or opening an existing project and copying the Project ID value. You can also get a list of existing projects and their IDs from the command line using the command `gradient projects list`.

For more information about this sample experiment see the README in the mnist-sample github repo: [https://github.com/Paperspace/mnist-sample](https://github.com/Paperspace/mnist-sample). Note: the code for this experiment can be run in both singlenode and multi-node training modes.

### Creating a multi-node experiment using the CLI

The following command creates and starts a multi-node experiment called `multiEx` and places it within the Gradient Project identified by the `--projectId` option. 

```bash
gradient experiments run multinode \
  --name multiEx \
  --projectId <your-project-id> \
  --experimentType GRPC \
  --workerContainer tensorflow/tensorflow:1.13.1-gpu-py3 \
  --workerMachineType K80 \
  --workerCommand "python mnist.py" \
  --workerCount 2 \
  --parameterServerContainer tensorflow/tensorflow:1.13.1-gpu-py3 \
  --parameterServerMachineType K80 \
  --parameterServerCommand "python mnist.py" \
  --parameterServerCount 1 \
  --workspaceUrl https://github.com/Paperspace/mnist-sample.git \
  --modelType Tensorflow
```

{% hint style="info" %}
Note: `--modelType Tensorflow` is will automatically parse and store the model's performance metrics and prepare it for [Deployment](../deployments/about.md) with TensorFlow Serving.
{% endhint %}

To run this command substitute an existing project ID for &lt;your-project-id&gt;. You can get an existing project id by going to [your projects list](https://www.paperspace.com/console/projects) and creating a new project or opening an existing project and copying the Project ID value. You can also get a list of existing projects and their IDs from the command line using the command `gradient projects list`.

The command above specifies the use of the gRPC framework and names the same Docker container, machine type, and programmatic command for both the 2 workers and the 1 parameter server.

Finally, the command specifies the workspace to pull the Python script from as a public GitHub repository.

For more information about this sample experiment see the README in the mnist-sample GitHub repo: [https://github.com/Paperspace/mnist-sample](https://github.com/Paperspace/mnist-sample). \(Note: the code for this experiment can be run in both singlenode and multinode training modes.\)

## Options common to both single-node and multi-node experiments

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
  --apiKey TEXT                API key to use this time only
  --help                       Show this message and exit
```

## Options specific to single-node experiments

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

Also, using the `--containerUser` option, you can specify a UNIX user name to be used as the UNIX identity for running the specified command in the container. If no `containerUser` is specified, the user will default to 'root' in the container. This is useful when running a public container image with a different expected user, or when building a container image from a Dockerfile.

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

In the case of multi-node experiments, both worker and parameter server instances need a container, machine type, command, count, and optionally a Docker registry username and password.

Note: `--containerUser` is not a supported option for multi-node experiments currently.

