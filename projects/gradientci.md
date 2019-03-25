---
description: Set up continuous integration between your GitHub repository and Gradient
---

# GradientCI

## Set Up GradientCI

### Creating a GradientCI Project via the Paperspace Console

To create a Gradient Project with continuous integration powered by GradientCI and GitHub:

1. Install the [GradientCI](https://github.com/apps/gradientci) GitHub app on your repository. \(GitHub Admin privilege is required.\)
2. Navigate to the [Projects page](https://www.paperspace.com/console/projects).
3. Click Create Project.
4. Select GitHub Project.
5. Grant Paperspace access to your GitHub repos via OAuth.
6. Confirm a repo with GradientCI installed for your new Gradient° Project.

### Configure GradientCI Settings

To set up GradientCI, our continuous integration service, include a directory in your GitHub repository called `.ps_project` with a configuration file `config.yaml`.

#### Template

```text
# .ps_project/config.yaml:

version: 0

project: "project-handle"
experiment: "experiment-name" [optional, default:<repo name>]
type: "experiment-type" [single|multi-grpc|multi-mpi]
ports: "5000" [optional, default:5000]
paths: [optional]
  workdir: "/path/to/workdir"
  artifacts: "/path/to/artifacts"
worker:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
  count: 1 [required for multi-node]
parameter-server: [required for multi-node]
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
  count: 1
```

#### Examples with only required fields

Single-node example

```text
version: 0

type: "single"
worker:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
```

Multinode example

```text
version: 0

type: "multi-grpc"
worker:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
  count: 2
parameter-server:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
  count: 1
```

#### Examples with optional fields included

Single-node example

```text
version: 0

project: "fko0j2xs3mqqi"
experiment: "momo/perfect-run"
type: "single"
ports: "5000"
paths:
  workdir: "/home/playground"
  artifacts: "/var/ml/artifacts"
worker:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
```

Multinode example

```text
version: 0

project: "fko0j2xs3mqqi"
experiment: "momo/perfect-runner"
type: "multi-grpc"
ports: "5000"
paths:
  workdir: "/home/playground"
  artifacts: "/var/ml/artifacts"
worker:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
  count: 2
parameter-server:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
  count: 1
```

