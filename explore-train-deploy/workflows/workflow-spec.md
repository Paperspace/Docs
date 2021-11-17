# Workflow Spec

This describes in more detail the main components of a Gradient Workflow, as seen in the YAML file.

## Key Concepts

### `defaults`

At the top of the YAML Workflow file, you can specify default parameters to be used throughout the entire Workflow. This includes environment variables and default machine instance configuration. Instances can also be specified per-job.

### `inputs`

The `inputs` block allows you to specify named inputs \(e.g., a [versioned dataset](../../data/data-overview/private-datasets-repository/)\) to be referenced and consumed by your jobs.

_Note:_ you can also collect inputs in a separate YAML and reference this file as an `inputPath` when creating a Workflow run.

Workflow and job-level inputs can be of type: dataset \(a persistent, versioned collection of data\), string \(e.g., a generated value or ID that may be output from another job\) or volume \(a temporary workspace mounted onto a job's container\).

_Note:_ datasets must be defined in advance of being referenced in a workflow. See [Create Datasets for the Workflow](https://docs.paperspace.com/gradient/explore-train-deploy/workflows/getting-started-with-workflows#create-datasets-for-the-workflow) for more information.

### `jobs`

Jobs are also sometimes referred to as "steps" within the Gradient Workflow. A job is an individual task that executes code \(such as a training a machine learning model\) and can consume inputs and produce outputs.

## Sample Workflow Spec

To run this Workflow, define datasets named `test-one`, `test-two`, and `test-three` as described in the [Create Datasets for the Workflow](https://docs.paperspace.com/gradient/explore-train-deploy/workflows/getting-started-with-workflows#create-datasets-for-the-workflow) documentation. Also, to make use of the secret named `hello` in the inputs section, define a secret as described [here](../../get-started/managing-projects/using-secrets.md).

```yaml
defaults:
  # Default environment variables for all jobs. Can use any supported
  # substitution syntax (named secrets, ephemeral secrets, etc.).
  env:
    # This environment variable uses a Gradient secret called "hello".
    HELLO: secret:hello
  # Default instance type for all jobs
  resources:
    instance-type: P4000

# Workflow takes two inputs, neither of which have defaults. This means that
# when the Workflow is run the corresponding input for these values are
# required, for example:
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
    # Workflow inputs.
    #
    # All inputs are placed in the "/inputs/<name>" path of the run
    # containers. So for this job we would have the paths "/inputs/data"
    # and "/inputs/echo".
    inputs:
      # The "/inputs/data" directory would contain the contents for the dataset
      # version. ID here refers to the name of the dataset, not its dataset ID.
      data: workflow.inputs.data
      # The "/inputs/echo" file would contain the string of the Workflow input
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
      # These inputs use job-1 outputs instead of Workflow inputs. You must
      # specify job-1 in the needs section to reference them here.
      data2: job-1.outputs.data2
      echo2: job-1.outputs.echo2
    outputs:
      data3:
        type: dataset
        with:
          ref: test-three
    # List of job IDs that must complete before this job runs
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

