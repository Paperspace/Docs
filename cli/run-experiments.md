# Run Experiments from the CLI

## How to run a single-node or multinode experiment

```
$ paperspace-python experiments create singlenode --help
Usage: paperspace-python experiments create singlenode [OPTIONS]

$ paperspace-python experiments create multinode --help
Usage: paperspace-python experiments create multinode [OPTIONS]
```

## Parameters common to both experiment types
```
Options:
  --name TEXT                  [required]
  --ports INTEGER
  --workspaceUrl TEXT
  --workingDirectory TEXT
  --artifactDirectory TEXT
  --cluster TEXT
  --experimentEnv JSON_STRING
  --triggerEventId TEXT
  --projectId TEXT
  --container TEXT             [required]
  --machineType TEXT           [required]
  --command TEXT               [required]
  --count INTEGER
  --containerUser TEXT
  --registryUsername TEXT
  --registryPassword TEXT
  --help 
```

* `--name` defines your experiment name.
* `--ports` defines what ports the experiment service accesses on the worker node.
* `--workspaceUrl` points to a workspace like a Git repository.
* `--workingDirectory` specifies the node's working directory.
* `--artifactDirectory` locates the directory in which the worker will place any outputs.
* `--cluster` defines what cluster the experiment will run on. (?)
* `--experimentEnv` = ?
* `--triggerEventID` defines an event that will trigger your experiment to run.
* `--projectId` specifies the Gradient Project to perform the experiment in.
* `--container` specifies what Docker container the worker node should use.
* `--machineType` specifies what kind of chip to use.
* `--command` tells the worker what script to execute.
* `--count` ? (should this even BE in single node?)
* `--containerUser` ?
* `--registryUsername` is your username if you're using a private Docker image.
* `--registryPassword` is your password if you're using a private Docker image.
* `--help` brings up the help menu.

## Special parameters for multinode experiments

```
Options
  --experimentType [GRPC|MPI] TEXT   [required]
  --workerContainer TEXT          [required]
  --workerMachineType TEXT        [required]
  --workerCommand TEXT            [required]
  --workerCount INTEGER           [required]
  --parameterServerContainer TEXT
                                  [required]
  --parameterServerMachineType TEXT
                                  [required]
  --parameterServerCommand TEXT   [required]
  --parameterServerCount INTEGER  [required]
  --workerContainerUser TEXT
  --workerRegistryUsername TEXT
  --workerRegistryPassword TEXT
  --parameterServerContainerUser TEXT
  --parameterServerRegistryContainerUser TEXT
  --parameterServerRegistryPassword TEXT
```

* `--experimentType` determines which protocol to use: gRPC or MPI.
* As above, both workers and parameters need a container, machine type, command, count, and registry. username and password.
