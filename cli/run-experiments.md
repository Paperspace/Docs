# Run Experiments from the CLI

Gradient supports [GitHub-integrated projects](../projects/gradientci.md) and standalone projects. In a standalone project, you can use the GUI experiment builder directly in the application, or the CLI, which enables you to run experiments manually and programmatically from your command line for maximum flexibility.

## How to run a single-node or multinode experiment

Use the `--help` flag to bring up information in your terminal.

```text
$ paperspace-python experiments create singlenode --help
Usage: paperspace-python experiments create singlenode [OPTIONS]

$ paperspace-python experiments create multinode --help
Usage: paperspace-python experiments create multinode [OPTIONS]
```

### Walkthrough of a multinode example

```text
$ paperspace-python experiments createAndStart multinode
  --name multiEx
  --projectId prjsrr8ee
  --experimentTypeId GRPC
  --workerContainer tensorflow/tensorflow:1.13.1-gpu-py3
  --workerMachineType K80
  --workerCommand "python mnist.py"
  --workerCount 2
  --parameterServerContainer tensorflow/tensorflow:1.13.1-gpu-py3
  --parameterServerMachineType K80
  --parameterServerCommand "python mnist.py"
  --parameterServerCount 1
  --workspaceUrl https://github.com/Paperspace/multinode-mnist.git
```

This command creates and starts a multinode experiment called `multiEx` and places it within the Gradient Project `prjsrr8ee`. \(To get your `projectId`, go to [your projects list](https://www.paperspace.com/console/projects) and copy it.\)

The command specifies the use of the gRPC framework and names the same Docker container, machine type, and programmatic command for both the 2 workers and the 1 parameter server.

Finally, the command specifies the workspace to pull the Python script from as a public GitHub repository.

## Parameters common to both experiment types

```text
Options:
  --name              TEXT        [required]  // Defines your experiment name.
  --ports             INTEGER                 // Defines what ports the experiment service accesses.
  --workspaceUrl      TEXT                    // Points to a workspace, such as a GitHub repository.
  --workingDirectory  TEXT                    // Specifies the node's working directory.
  --artifactDirectory TEXT                    // Locates the directory in which the worker will place any outputs.
  --cluster           TEXT                    // Defines what cluster the experiment will run on.
  --experimentEnv     JSON_STRING             // ?
  --triggerEventId    TEXT                    // Defines an event that will trigger your experiment to run, like a Git commit.
  --projectId         TEXT                    // Specifies the Gradient Project to perform the experiment in.
  --container         TEXT         [required] // Specifies what Docker container the worker node should use.
  --machineType       TEXT         [required] // Specifies what kind of chip to use.
  --command           TEXT         [required] // Tells the worker what script to execute.
  --count             INTEGER                 // ?
  --containerUser     TEXT                    // ? (duplicate of `registryUsername`?)
  --registryUsername  TEXT                    // Your username, if you're using a private Docker image.
  --registryPassword  TEXT                    // Your password, if you're using a private Docker image.
  --help                                      // Brings up the help menu.
```

## Special parameters for multinode experiments

```text
Options
  --experimentType    TEXT [GRPC|MPI] [required] // Determines which protocol to use: gRPC or MPI.
  --workerContainer   TEXT            [required]
  --workerMachineType TEXT            [required]
  --workerCommand     TEXT            [required]
  --workerCount       INTEGER         [required]
  --parameterServerContainer   TEXT   [required]
  --parameterServerMachineType TEXT   [required]
  --parameterServerCommand     TEXT   [required]
  --parameterServerCount     INTEGER  [required]
  --workerContainerUser        TEXT             // ?
  --workerRegistryUsername     TEXT
  --workerRegistryPassword     TEXT
  --parameterServerContainerUser TEXT           // ?
  --parameterServerRegistryContainerUser TEXT
  --parameterServerRegistryPassword TEXT
```

As above, both workers and parameters need a container, machine type, command, count, and registry username and password.

