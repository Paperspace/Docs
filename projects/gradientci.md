---
description: Set up continuous integration between your GitHub repository and Gradient
---

# GradientCI

## Set Up GradientCI

To set up GradientCI, our continuous integration service, include a directory in your GitHub repository called `.ps_project` with a configuration file `config.yaml`.

## Template

```text
# .ps_project/config.yaml:

version: 1

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

### Examples with only required fields

#### Single-node example

```text
version: 1

type: "single"
worker:
  container: "tensorflow/tensorflow:1.8.0-gpu"
  command: "nvidia-smi"
  machine-type: "K80"
```

#### Multinode example

```text
version: 1

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

### Examples with optional fields included

#### Single-node example

```text
version: 1

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

#### Multinode example

```text
version: 1

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

