# Workflow Spec

## Key Concepts

### `defaults`

At the top of the yaml workflow file  you can specify default parameters to be used throughout the entire workflow. This includes environment variables, default machine instance configuration.

### `inputs`

The `inputs` block allows you to specify versioned dataset to be referenced and consumed by your jobs. Note, you can also collect these in a separate `inputs.yaml` file and reference this file when creating a workflow run.

### `jobs`

Jobs are also sometimes referred to as "steps" within the Gradient Workflow. A job is an individual task that executes code \(such as a training a machine learning model\) and can produce outputs \(i.e. versioned datasets\). 

## Sample Workflow Spec

```yaml
defaults:
  # default environment variables for all jobs, can use any supported
  # substitution syntax (named secrets, ephemeral secrets, etc...)
  env:
    HELLO: secret:hello
  # default instance type for all jobs
  resources:
    instance-type: metal-cpu

# workflow takes two inputs, neither of which have defaults. This means that
# when the workflow is run corresponding input corresponding for these values
# are required, example:
#
# {"inputs": {"echo": {"value": "hello world"}, "data": {"id": "test-one"}}}
#
inputs:
  data:
    type: dataset
  echo:
    type: string

jobs:
  job-1:
    # These are inputs for the "job-1" job, they are "aliases" to the
    # workflow inputs
    #
    # All inputs are placed in the "/inputs/<name>" path of the run
    # containers. So for this job we would have the paths "/inputs/data"
    # and "/inputs/echo".
    inputs:
      # The "/inputs/data" directory would contain the contents for the dataset
      # version.
      data: workflow.inputs.data
      # The "/inputs/echo" file would contain the string of the workflow input
      # "echo".
      echo: workflow.inputs.echo
     # These are outputs for the "job-1" job.
    #
    # All outputs are read from the "/outputs/<name>" path.
    outputs:
       # A directory will automatically be created for output datasets and
      # any content written to that directory will be committed to a newly
      # created dataset version when the jobs completes.
      data2:
        type: dataset
        with:
          id: test-two
       # The container is responsible creating th file "/outputs/<name>" with the
      # content being a small-ish utf-8 encoded string.
      echo2:
        type: string
     # Set job specific environment variables
    env:
      FOOBAR: test
    # Set action
    uses: container@v1
    # Set action arguments
    with:
      args:
      - bash
      - -c
      - find /inputs/data > /outputs/data2/list.txt; echo ENV $HELLO $FOOBAR > /outputs/echo2
      image: bash:5
  job-2:
    inputs:
      # these inputs use job-1 outputs instead of workflow inputs, you must
      # specify job-1 in the needs section to reference them here
      data2: job-1.outputs.data2
      echo2: job-1.outputs.echo2
    outputs:
      data3:
        type: dataset
        with:
          id: test-three
    # List of job-id's that must complete before this job runs
    needs:
    - job-1
    uses: container@v1
    with:
      args:
      - bash
      - -c
      - wc -l /inputs/data2/list.txt > /outputs/data3/summary.txt
      image: bash:5
```

## Example Workflow Run Output

```javascript
{
    "cluster": {
        "id": "cla7rjbzg"
    },
    "id": 1,
    "spec": {
        "defaults": {
            "env": {
                "HELLO": "secret:hello"
            },
            "resources": {
                "instance-type": "metal-cpu"
            }
        },
        "inputs": {
            "data": {
                "type": "dataset"
            },
            "echo": {
                "type": "string"
            }
        },
        "jobs": {
            "job-1": {
                "env": {
                    "FOOBAR": "test"
                },
                "inputs": {
                    "data": "workflow.inputs.data",
                    "echo": "workflow.inputs.echo"
                },
                "outputs": {
                    "data2": {
                        "type": "dataset",
                        "with": {
                            "id": "test-two"
                        }
                    },
                    "echo2": {
                        "type": "string"
                    }
                },
                "uses": "container@v1",
                "with": {
                    "args": [
                        "bash",
                        "-c",
                        "find /inputs/data > /outputs/data2/list.txt; echo ENV $HELLO $FOOBAR > /outputs/echo2"
                    ],
                    "image": "bash:5"
                }
            },
            "job-2": {
                "inputs": {
                    "data2": "job-1.outputs.data2",
                    "echo2": "job-1.outputs.echo2"
                },
                "needs": [
                    "job-1"
                ],
                "outputs": {
                    "data3": {
                        "type": "dataset",
                        "with": {
                            "id": "test-three"
                        }
                    }
                },
                "uses": "container@v1",
                "with": {
                    "args": [
                        "bash",
                        "-c",
                        "wc -l /inputs/data2/list.txt > /outputs/data3/summary.txt; cat /inputs/echo2"
                    ],
                    "image": "bash:5"
                }
            }
        }
    },
    "status": {
        "finished": "2020-12-31T22:50:47.000Z",
        "inputs": {
            "data": {
                "dataset": {
                    "id": "test-one:qdwlyje"
                },
                "with": {
                    "id": "test-one"
                }
            },
            "echo": {
                "with": {
                    "value": "hello world"
                }
            }
        },
        "jobs": {
            "job-1": {
                "finished": "2020-12-31T22:50:33.000Z",
                "logId": "wfrjb704734fbbd24348894fa0f0ffb10581",
                "outputs": {
                    "data2": {
                        "dataset": {
                            "id": "test-two:zfk5vqx",
                            "isCommitted": true
                        }
                    }
                },
                "phase": "SUCCEEDED",
                "started": "2020-12-31T22:50:30.000Z"
            },
            "job-2": {
                "finished": "2020-12-31T22:50:39.000Z",
                "logId": "wfrj2d106a58ee7b4e66b0bd26946a43db5f",
                "outputs": {
                    "data3": {
                        "dataset": {
                            "id": "test-three:atef63i",
                            "isCommitted": true
                        }
                    }
                },
                "phase": "SUCCEEDED",
                "started": "2020-12-31T22:50:34.000Z"
            }
        },
        "logId": "wfr31c0dbeae5d347cba4ff3690c9f36888",
        "phase": "SUCCEEDED",
        "started": "2020-12-31T22:50:25.000Z"
    }
}
```

