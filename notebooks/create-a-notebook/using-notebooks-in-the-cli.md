# Using Notebooks in the CLI

The Notebooks section of the [CLI](../../get-started/install-the-cli.md) currently provides the ability to manage and inspect Notebooks.

```text
Usage: gradient notebooks [OPTIONS] COMMAND [ARGS]...

  Manage notebooks

Options:
  --help  Show this message and exit.

Commands:
  artifacts  Manage notebooks' artifacts
  create     Create new notebook
  delete     Delete existing notebook
  details    Show notebook details
  fork       Fork existing notebook
  list       List notebooks
  metrics    Read notebook metrics
  start      Start notebook
  stop       Stop running notebook
  tags       Manage notebook tags
```

## Creating a notebook

Notebooks are created by default in the public SaaS clusters.
Enterprise users may specify their private cluster.
Notebooks, unlike experiments and jobs, are started immediately on creation.

```
Usage: gradient notebooks create [OPTIONS]

  Create new notebook

Options:
  --machineType TEXT              Virtual Machine type label e.g. P5000
                                  [required]

  --container TEXT                Container name  [required]
  --clusterId TEXT                Cluster ID
  --name TEXT                     Notebook name
  --registryUsername TEXT         Registry username
  --registryPassword TEXT         Registry password
  --command TEXT                  Command (executed as `/bin/sh -c 'YOUR
                                  COMMAND'`)

  --containerUser TEXT            Container user
  --shutdownTimeout INTEGER       Shutdown timeout in hours
  --isPreemptible                 Is preemptible
  --isPublic                      Is publically viewable
  --environment JSON_STRING       Environmental variables
  --workspace TEXT                S3 url or git repository. Directory uploads
                                  are not yet supported

  --workspaceRef TEXT             Git commit hash, branch name or tag
  --workspaceUsername <username>
  --workspacePassword TEXT        Workspace password
  --tag TEXT                      One or many tags that you want to add to
                                  experiment

  --tags TEXT                     Separated by comma tags that you want add to
                                  experiment

  --apiKey TEXT                   API key to use this time only
  --optionsFile PATH              Path to YAML file with predefined options
  --createOptionsFile PATH        Generate template options file
  --help                          Show this message and exit..
```

## Starting a Notebook

You may start a _stopped_ notebook again.
The notebook can be started on a different cluster or machine type.

```
Usage: gradient notebooks start [OPTIONS]

  Start notebook

Options:
  --id TEXT                  Notebook ID  [required]
  --machineType TEXT         Virtual Machine type label e.g. P5000
                             [required]

  --clusterId TEXT           Cluster ID
  --name TEXT                Notebook name
  --shutdownTimeout INTEGER  Shutdown timeout in hours
  --isPreemptible            Is preemptible
  --tag TEXT                 One or many tags that you want to add to
                             experiment

  --tags TEXT                Separated by comma tags that you want add to
                             experiment

  --apiKey TEXT              API key to use this time only
  --optionsFile PATH         Path to YAML file with predefined options
  --createOptionsFile PATH   Generate template options file
  --help                     Show this message and exit.
```

## Forking a Notebook

Forking a notebook creates a new history for your notebook.
This can copy notebooks, including public notebooks, into a team.
After the fork there will be a stopped notebook created in your team you must call `gradient notebooks start --id ID` to run it.

```
Usage: gradient notebooks fork [OPTIONS]

  Fork existing notebook

Options:
  --id TEXT                 Notebook ID
  --apiKey TEXT             API key to use this time only
  --optionsFile PATH        Path to YAML file with predefined options
  --createOptionsFile PATH  Generate template options file
  --help                    Show this message and exit.
```
