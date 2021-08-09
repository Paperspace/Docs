# Workflow Spec

## Key Concepts

### `defaults`

At the top of the yaml workflow file, you can specify default parameters to be used throughout the entire workflow. This includes environment variables and default machine instance configuration.

### `inputs`

The `inputs` block allows you to specify named inputs \(e.g. a [versioned dataset](../../data/data-overview/private-datasets-repository/)\) to be referenced and consumed by your jobs. Note: you can also collect inputs in a separate yaml and reference this file as an `inputPath` when creating a workflow run.

Workflow and job-level inputs can be of type: dataset \(a persistent, versioned collection of data\), string \(e.g. a generated value or ID that may be outputted from another job\) or volume \(a temporary workspace mounted onto a job's container\). Note: datasets must be defined in advance of being referenced in a workflow. See the [dataset](../../data/data-overview/) documentation for more info.

### `jobs`

Jobs are also sometimes referred to as "steps" within the Gradient Workflow. A job is an individual task that executes code \(such as a training a machine learning model\) and can consume inputs and produce outputs.

## Sample Workflow Spec

To run this workflow, define datasets named 'test-one', 'test-two', and 'test-three' as described in the [dataset](../../data/data-overview/) documentation. Also, to make use of the secret named 'hello' in the inputs section, define a secret as described [here](../../get-started/managing-projects/using-secrets.md).

```yaml
defaults:
  # default environment variables for all jobs, can use any supported
  # substitution syntax (named secrets, ephemeral secrets, etc...)
  env:
    # this env var uses a Gradient secret called "hello"
    HELLO: secret:hello
  # default instance type for all jobs
  resources:
    instance-type: P4000

# workflow takes two inputs, neither of which have defaults. This means that
# when the workflow is run corresponding input for these values are required,
# for example:
#
# {"inputs": {"data": {"id": "test-one"}, "echo": {"value": "hello world"}}}
#
inputs:
  data:
    type: dataset
    with:
      ref: test-one
  echo:
    type: string
    with:
      value: "hello world"
jobs:
  job-1:
    # These are inputs for the "job-1" job; they are "aliases" to the
    # workflow inputs
    #
    # All inputs are placed in the "/inputs/<name>" path of the run
    # containers. So for this job we would have the paths "/inputs/data"
    # and "/inputs/echo".
    inputs:
      # The "/inputs/data" directory would contain the contents for the dataset
      # version. id here refers to the name of the dataset, not its dataset id.
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
      # The container is responsible creating the file "/outputs/<name>" with the
      # content being a small-ish utf-8 encoded string.
      echo2:
        type: string
    # Set job-specific environment variables
    env:
      TSTVAR: test
    # Set action
    uses: container@v1
    # Set action arguments
    with:
      args:
      - bash
      - -c
      - find /inputs/data > /outputs/data2/list.txt; echo ENV $HELLO $TSTVAR > /outputs/echo2; cat /inputs/echo; echo; cat /outputs/data2/list.txt /outputs/echo2
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
          ref: test-three
    # List of job-id's that must complete before this job runs
    needs:
    - job-1
    uses: container@v1
    with:
      args:
      - bash
      - -c
      - wc -l /inputs/data2/list.txt > /outputs/data3/summary.txt; cat /outputs/data3/summary.txt /inputs/echo2
      image: bash:5
```
