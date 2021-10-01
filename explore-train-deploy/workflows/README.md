---
description: Automate from idea to production
---

# Workflows

Workflows are the newest \(and most powerful\) way to create machine learning projects. Workflows let you use a [GitHub-action](https://docs.github.com/en/actions) style syntax via [YAML](https://en.wikipedia.org/wiki/YAML) files to easily create powerful automation.

Workflows allow you to build complex, real-world machine learning projects. Note, this is an advanced topic so if you are still early in your ML journey, it might make more sense to start with [Notebooks](../../get-started/tutorials-list/getting-started-with-gradient-notebooks-old.md) first.

Workflows are based on the [Argo runtime engine](https://github.com/argoproj/argo-workflows#what-is-argo-workflows) which is a container-native continuous delivery tool for Kubernetes.

![Gradient Workflows &#x2014; Automate from idea to production](../../.gitbook/assets/screen-shot-2021-06-16-at-11.17.23-am.png)

## Key Terminology

* **Workflow**: a named or unnamed entity that belongs to a team and project
  * Named workflows can be re-run with a default `workflow spec`, or be passed a new spec every time
* [**Workflow Spec**](workflow-spec.md): a YAML list of jobs that is converted into an Argo template and run on the Gradient distributed runtime engine.
* [**Job**](workflow-spec.md#jobs): self-contained part of a workflow spec that is similar to an Argo step
  * Jobs can define inputs, outputs, and their own environment variables
  * Jobs can require other jobs via "needs" and collect/pass info between jobs
  * Jobs can be implemented with an action via "use"
* [**Action**](gradient-actions.md): a self-contained, composable set of code building blocks that can perform specific actions within a machine learning project. 
  * Actions can receive parameters \(e.g., args, image\) within the job step via the "with" argument
  * E.g., `container@v1` action = run a container, load inputs, and produce outputs
* [**Workflow Run**](workflow-spec.md#example-workflow-run-output): the implementation of a workflow
  * The most basic run requires a `workflowId` and `clusterId` - most will also include a workflowSpec, and the inputs to be passed into the workflow
  * The workflow run contains everything needed for the workflow to actually be executed, i.e., what \(`workflowId`\), where \(`clusterId`\), how \(`workflowSpec`\), with \([inputs](workflow-spec.md#inputs), etc.\)

