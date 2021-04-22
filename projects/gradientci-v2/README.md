---
description: Set up continuous integration between your GitHub repository and Gradient
---

# GradientCI

![gradientci logo](../../.gitbook/assets/gradientci%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%281%29.gif)

## Set Up GradientCI

### Creating a GradientCI Project via the Paperspace Console

To create a Gradient Project with continuous integration powered by GradientCI and GitHub:

1. Install the [GradientCI](https://github.com/apps/gradientci) GitHub app on your repository.

   \(GitHub Admin privilege is required.\)

2. Navigate to the [Projects page](https://www.paperspace.com/console/projects).
3. Click Create Project.
4. Select GitHub Project.
5. Grant Paperspace access to your GitHub repos via OAuth.
6. Confirm a repo with GradientCI installed for your new Gradient° Project.

### Configure GradientCI Settings

To set up GradientCI, our continuous integration service, include a directory in your GitHub repository called `.ps_project` with a configuration file `config.yaml`, examples below.

### Building Branches and Tags

GradientCI supports building and sourcing project configuration from arbitrary branches or tags. By default we only build configuration sourced from your default branch \(typically `master`\). You can [change your repositories default branch from within Github](https://help.github.com/en/articles/setting-the-default-branch), if you only need the configuration from one branch. You can relax or tighten this rule by selecting "All" or "None" from the "Build Branches" dropdown in the project settings pane of the Gradient console. If you would like to build any tags or a subset of branches that are not the default branch, select "All" from this menu and provide filters in your `config.yaml`. To list the specific patterns of tags and branches to build, see [branch and tag triggers](gradientci-v2.md#branches-and-tags).

You may additionally disable the builds of pull requests, enabled by default. Or enable builds of pull requests that originate from forked repositories, disabled by default to prevent unauthorized use of Gradient resources. Each of these options will allow configuration to be sourced from the relevant Git branch.

![Gradient console project settings pane](../../.gitbook/assets/project-settings.png)

#### Template

```yaml
# .ps_project/config.yaml:

version: 2

workflows:
  experiment-workflow:
    steps:
      -
        name: "my-experiment"
        command: experiment.run_single_node
        params:
          command: python mnist.py
          container: tensorflow/tensorflow:1.13.1-gpu-py3
          experimentEnv:
            EPOCHS_EVAL: 5
            EVAL_SECS: 10
            MAX_STEPS: 1000
            TRAIN_EPOCHS: 10
          machineType: P4000
          modelPath: /artifacts
          modelType: Tensorflow
          name: mnist-cli-config-yaml
        checks: #[optional]
          onnx:loss:
            target: "0.0..0.5"
            aggregate: "mean"
          defaults: #[optional]
            precision: 3
      triggers:
        branches:
          ignore: irrelevant-branch
        tags:
          only:
            - v.*
            - latest
  param-file-experiment-workflow:
    steps:
      -
        name: "param-file-experiment"
        command: experiment.run_single_node
        paramsFile: .ps_project/param-file-experiment.yml
        checks: #[optional]
          custom:loss:
            target: "0.0..0.5"
            aggregate: "/mean/0"
      triggers:
        branches:
          only: master
```

## Workflows

Your CI configuration is separated into individual workflows. Workflows are named units of work that are executed in parallel. A workflow is comprised of a [`triggers`](gradientci-v2.md#triggers) block and a series of [`steps`](gradientci-v2.md#steps) to execute.

### Steps

Steps are a series of sequentially executed actions. These generally correspond to actions available in the Paperspace CLI/SDK. _Currently, only one step per workflow is supported._ For complex pipelines you may run a single node experiment that contains a python script with a series of Paperspace SDK calls to orchestrate your pipeline. The SDK Pipeline style offers more flexibility than can be described by the yaml pipeline configuration as you can describe complex logic using plain python code. SDK pipelines offer the latest SDK functionality as soon as it becomes available, often before it can be integrated into the yaml pipeline syntax. For an example see [SDK Pipeline.](https://github.com/Paperspace/Docs/tree/dace77bbd70b824f1dfd4bf27fc24deef5218d16/projects/gradentci-v2.md#examples)

#### Required Properties

* `name`: a string identifier for the step, often used in reporting results.

  This name must be unique amongst the steps for a workflow.

* `command`: what type of step should be executed.

  These match the qualified names in the Paperspace SDK.

  Supported commands:

  * `experiment.run_single_node`
  * `experiment.run_multi_node`
  * `experiment.run_mpi_multi_node`

* One of `params` or `paramsFile`
  * `paramsFile`: a path to file contained in your project repository containing the yaml arguments for the step.

    These are the same as those generated by the CLI, see the experiments [config documentation](https://github.com/Paperspace/Docs/tree/dace77bbd70b824f1dfd4bf27fc24deef5218d16/experiments/gradient-config.yaml.md) for an example of one of these files and further documentation.

  * `params` this is a object with the parameters for the relevant step.

    These are the same as the contents of a `paramsFile` inlined into your `.ps_projects/config.yaml`.

#### Optional Properties

* `checks`: these configure status checks on your GitHub pull requests.

  See [Metrics Checks](gradientci-v2.md#metrics-checks) for the full schema.

### Triggers

#### Branches and Tags

By default GradientCI will only build the default branch and no tags. If you would like to build additional non-pull request branches or tags you must select "All" from the "Build Branches" project configuration dropdown. This will build all branches and no tags. Once that is complete you can filter additional branches in your `config.yaml` by providing a `triggers` section. You can place the keys `branches` or `tags` to apply filters to the default. Under each key you can provide `only` or `ignore` fields, but not both, containing a [POSIX compatible regex](https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions) or array of regex to match on. Branches or tags filtered by an `only` key must match one or more of the regex provided. Branches or tags filtered by an `ignore` key will be skipped if they match one or more of the regex provided.

### Metrics Checks

The GradientCI service can help you from degrading your model. When you run an experiment based on a code change, GradientCI can automatically check properties of the experiment and forward those results to GitHub. GitHub can use these statuses to prevent pull requests merges that degrade your model. GradientCI will automatically report whether the experiment ran without error or which checks failed if there was an error. You may configure additional checks for metrics that are generated by your experiment under the `checks` key in your `config.yaml`. Currently, we only support scalar metrics coming from TensorFlow generated summaries.

In addition to the status checks, GradientCI writes a detailed summary of the experiment to a comment on the pull request so you have your critical data at a glance while reviewing code.

![GitHub pull request blocked by failing GradientCI metric checks.](../../.gitbook/assets/pr-status.png)

#### GitHub Configuration

For best results, especially on repositories with many contributors, we recommend configuring GitHub branch protections to prevent accidental merges of unintended pull requests. After your first build, statuses for the metrics will be reported back and you can make passing statuses required for the merge of your pull request. To do this follow [GitHub's documentation.](https://help.github.com/en/articles/configuring-protected-branches)

#### Checks Schema

```yaml
# ...
checks:
  <identifier>:
    target: <range> #[required]
    aggregate: mean #[required]
    round: down #[optional, default: down, up|down]
    precision: 2 #[optional, default: 2]
    only-pulls: false #[optional, default: false]
    if-not-found: failure #[optional, default: "failure", success|failure]
    comment-on-pr: true #[optional, default: true]
  defaults:
    round: down #[optional, default: down, up|down]
    precision: 2 #[optional, default: 2]
    only-pulls: false #[optional, default: false]
    if-not-found: failure #[optional, default: "failure", success|failure]
    comment-on-pr: true #[optional, default: true]
```

#### `<identifier>`s:

* `<identifiers>` are split into two parts: 1. the source of the metric and 2. the name of the metric, e.g. `tensorflow:loss`.

  Supported `<identifiers>` are:

  * `tensorflow`
  * `onnx`
  * `custom`

* These `<identifiers>` are case-_sensitive_
* `“defaults”`: reserved for defaults to set for the `<identifiers>`.

  Any of the above keys are valid within this block and will set the default behavior for all other `<identifier>` blocks.

  If `round` is set to `down` all other metrics will be evaluated using the round down behavior.

  If an `<identifier>` has a key specified underneath it it will override the value in the `defaults` block.

  For instance, `round: up` under `tensorflow:loss` will override the `round: down` behavior in the `defaults` block.

#### `<range>`

Ranges can appear in the following forms:

1. `<number>` or `<number>..` this form allows you to specify that the metric must be greater than `<number>`.
2. `..<number>` this form allows you to specify that the metric must be less than `<number>`.
3. `<left>..<right>` this form allows you to specify that the metric must be less than `<left>` but greater than `<right>`.

Note these numbers are parsed as floats and relying on precise equality with the ends of the range is not recommended.

#### Required Properties

* `target`: this is a `<range>` for the metric to appear in
* `aggregate`: this is the aggregating function to evaluate the metric by.
  * These are objects emitted from your model summary, for tensorflow valid aggregates are:
    * `mean`
    * `stddev`
    * `max`
    * `min`
    * `var`
    * `median`
  * If the `<identifier>` is `custom`, the `aggregate` is evaluated as a [JSON pointer](https://tools.ietf.org/html/rfc6901)
    * These paths must begin with `/`
    * For example the mean of loss in `{"loss": { "mean": 0.5 }}` would be accessed with `/loss/mean`
    * For example the 2nd element in the loss array in `{"loss": [0.0, 0.5] }` would be accessed with `/loss/1`

#### Optional Properties

* `precision`: how many decimal places to keep \(default 2\)
* `round`: specifies rounding behavior \(default “down”\)
* `only-pulls`: only perform this check on pull requests
* `if-not-found`: return a default status if job has no data for `<identifier>`, defaults to “failure”
* `comment-on-pr`: include this metric in a summary content if the metrics were generated from a pull-request

## Job Environment

For some `step`s in your job GradientCI will automatically set environment variables so you can determine the triggering condition. These variables are currently set for `experiment.*` steps only.

* `PS_GRADIENT_CI_GIT_REF` the branch or tag that triggered the build
* `PS_GRADIENT_CI_GIT_SHA` the git commit currently being built
* `PS_GRADIENT_CI_GIT_REPO_URL` the repository that received the trigger.

  Note that builds from forks will appear to come from the _target_ repository, not the fork.

## S3 Datasets

We highly recommend the use of secrets on datasets as these get stored as plain text. You may set secrets on Cluster, Project, and/or Team level. If the same secret name is created for more than one scope only one will be applied. Secrets have the following precedence: Cluster &gt; Project &gt; Team. You can learn more about setting and using secrets [here](https://docs.paperspace.com/gradient/secrets/using-secrets).

## Examples

### Repositories

* [MNIST in TensorFlow](https://github.com/paperspace/mnist-sample)
* [SDK Pipeline](https://github.com/paperspace/TBD)

### Examples with only required fields

#### Single-node

```yaml
version: 2

workflows:
  single-node:
    steps:
      -
        name: "single-node"
        command: experiment.run_single_node
        params:
          command: nvidia-smi
          container: tensorflow/tensorflow:1.13.1-gpu-py3
          machineType: "K80"
```

#### Multi-Node

```yaml
version: 2

workflows:
  multi-node:
    steps:
      -
        name: "multi-node"
        command: experiment.run_multi_node
        params:
          workerCommand: nvidia-smi
          workerContainer: tensorflow/tensorflow:1.13.1-gpu-py3
          workerMachineType: "K80"
          workerCount: 2
          parameterServerCommand: nvidia-smi
          parameterServerContainer: tensorflow/tensorflow:1.13.1-gpu-py3
          parameterServerMachineType: "K80"
          parameterServerCount: 1
```

### Examples with \(some\) optional fields included

#### Single-node

```yaml
version: 2

workflows:
  single-node:
    steps:
      -
        name: "single-node"
        command: experiment.run_single_node
        params:
          command: nvidia-smi
          machineType: "K80"
          ports: "5000"
          workingDirectory: "/home/playground"
          artifactDirectory: "/artifacts"
          container: tensorflow/tensorflow:1.13.1-gpu-py3
          datasetUri: "https://some_other_uri/uri"
          datasetAwsAccessKeyId: "secret:<some_secret_name>"
          datasetAwsSecretAccessKey: "secret:<some_other_secret_name>"
```

#### Multi-Node

```yaml
version: 2

workflows:
  single-node:
    steps:
      -
        name: "single-node"
        command: experiment.run_multi_node
        params:
          workerCommand: nvidia-smi
          workerMachineType: "K80"
          workerWorkingDirectory: "/home/playground"
          workerArtifactDirectory: "/artifacts"
          workerContainer: tensorflow/tensorflow:1.13.1-gpu-py3
          parameterServerCommand: nvidia-smi
          parameterServerMachineType: "K80"
          parameterServerWorkingDirectory: "/home/playground"
          parameterServerArtifactDirectory: "/artifacts"
          parameterServerContainer: tensorflow/tensorflow:1.13.1-gpu-py3
```

#### TensorFlow Model Summary Checks

```yaml
version: 2

workflows:
  single-node:
    steps:
      -
        name: "single-node"
        command: experiment.run_single_node
        params:
          command: nvidia-smi
          machineType: "K80"
          ports: "5000"
          workingDirectory: "/home/playground"
          artifactDirectory: "/artifacts"
          container: tensorflow/tensorflow:1.13.1-gpu-py3
        modelType: "Tensorflow"
        modelPath: "/storage/models"
      checks:
        defaults:
          precision: 3
          round: up
          only-prs: true
        tensorflow:accuracy:
          target: 0.7..
          aggregation: mean
        tensorflow:loss:
          target: ..0.025
          aggregation: max
```

## Uninstalling GradientCI

Note this can only be done by an organization level administrator or on your personal repositories.

1. Navigate to the repository or organization that you wish to remove GradientCI from.
2. Click the "Settings" tab in the top row
3. Select "Integration & services" from the left menu, you should be presented with a list that includes "GradientCI" that looks like

   ![Integration &amp; services pane](../../.gitbook/assets/settings-pane.png)

4. Select "Configure" next to "GradientCI", you will be prompted to enter your password.
5. From the "GradientCI" settings menu, you can then either ![GradientCI Settings](../../.gitbook/assets/gradient-ci-settings.png)

   a. Uninstall the application from all repositories on the organization or personal account by clicking the red "Uninstall" button

   b. Select the "Only select repositories" and choosing which repositories should have GradientCI from the dropdown, or unselecting them by clicking the "x" next to their name.

## Troubleshooting

### Project Setup Incomplete

This error occurs when GradientCI is unable to find the attached Paperspace project for your GitHub repository. The Paperspace project may have been deleted or you may have installed the app only through GitHub's interface. Follow the [GradientCI project setup instructions](../managing-projects.md#create-a-gradient-ci-project) to ensure that your Paperspace project is properly configured.

