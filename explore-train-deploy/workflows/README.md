---
description: Gradient Workflows provides a simple way to automate machine learning tasks.
---

# Gradient Workflows

## Overview

Gradient Workflows is a new and powerful way to build-out machine learning applications. Workflows utilize  [GitHub-action](https://docs.github.com/en/actions) style syntax via [YAML](https://en.wikipedia.org/wiki/YAML) files to easily create powerful automation.

Workflows is based on the [Argo runtime engine](https://github.com/argoproj/argo-workflows#what-is-argo-workflows), which is a container-native continuous delivery tool for Kubernetes, and makes it easy to build complex and scalable projects with an arbitrary number of discrete steps.&#x20;

![Examining the logs from a simple workflow.](<../../.gitbook/assets/reading workflow logs dark.gif>)

Workflows is used by ML Engineers to build-out deterministic machine learning pipelines.&#x20;

## Where to start

The best tutorial is the canonical Gradient Workflows Tutorial:

{% content-ref url="../../get-started/tutorials-list/gradient-workflows-tutorial.md" %}
[gradient-workflows-tutorial.md](../../get-started/tutorials-list/gradient-workflows-tutorial.md)
{% endcontent-ref %}



![Gradient Workflows — Automate from idea to production](../../.gitbook/assets/screen-shot-2021-06-16-at-11.17.23-am.png)

## Key Terminology

* **Workflow**: a named or unnamed entity that belongs to a team and project
  * Named workflows can be re-run with a default `workflow spec`, or be passed a new spec every time
* [**Workflow Spec**](workflow-spec.md): a YAML list of jobs that is converted into an Argo template and run on the Gradient distributed runtime engine.
* [**Job**](workflow-spec.md#jobs): self-contained part of a workflow spec that is similar to an Argo step
  * Jobs can define inputs, outputs, and their own environment variables
  * Jobs can require other jobs via "needs" and collect/pass info between jobs
  * Jobs can be implemented with an action via "use"
* [**Action**](gradient-actions.md): a self-contained, composable set of code building blocks that can perform specific actions within a machine learning project.&#x20;
  * Actions can receive parameters (e.g., args, image) within the job step via the "with" argument
  * E.g., `container@v1` action = run a container, load inputs, and produce outputs
* [**Workflow Run**](workflow-spec.md#example-workflow-run-output): the implementation of a workflow
  * The most basic run requires a `workflowId` and `clusterId` - most will also include a workflowSpec, and the inputs to be passed into the workflow
  * The workflow run contains everything needed for the workflow to actually be executed, i.e., what (`workflowId`), where (`clusterId`), how (`workflowSpec`), with ([inputs](workflow-spec.md#inputs), etc.)
