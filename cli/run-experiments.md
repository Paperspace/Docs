# Run Experiments from the CLI

```
$ paperspace-python experiments create singlenode --help
Usage: paperspace-python experiments create singlenode [OPTIONS]


Options:
  --name TEXT                  [required]
  --ports INTEGER
  --workspaceUrl TEXT
  --workingDirectory TEXT
  --artifactDirectory TEXT
  --clusterId INTEGER
  --experimentEnv JSON_STRING
  --triggerEventId INTEGER
  --projectId INTEGER
  --projectHandle TEXT
  --container TEXT             [required]
  --machineType TEXT           [required]
  --command TEXT               [required]
  --count INTEGER
  --containerUser TEXT
  --registryUsername TEXT
  --registryPassword TEXT
  --help 


$ paperspace-python experiments create multinode --help
Usage: paperspace-python experiments create multinode [OPTIONS]


Options:
  --name TEXT                     [required]
  --ports INTEGER
  --workspaceUrl TEXT
  --workingDirectory TEXT
  --artifactDirectory TEXT
  --clusterId INTEGER // cluster TEXT
  --experimentEnv JSON_STRING
  --triggerEventId INTEGER // triggerEvent TEXT (?) // triggerEventId TEXT (if it has a handle, will be that)
  --projectId INTEGER // projectId TEXT (will actually be what we call the “handle”)
  --projectHandle TEXT // delete
  --experimentTypeId [GRPC|MPI]   [required] // experimentType TEXT
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
  --projectHandler TEXT
  --workerContainerUser TEXT
  --workerRegistryUsername TEXT
  --workerRegistryPassword TEXT
  --parameterServerContainerUser TEXT
  --parameterServerRegistryContainerUser TEXT
  --parameterServerRegistryPassword TEXT
  --help                          Show this message and exit.
```
