# Overview

A Gradient Project is a workspace for you or your team to run Experiments and Jobs, store Artifacts such as Models, and manage Deployments \(deployed models\). You can create a basic "standalone" project or a [GradientCI](gradientci.md) project which provides more advanced CI/CD pipelining capabilities.

With **Standalone Projects,** you submit Experiments from the UI or CLI manually. To create a standalone Project via the Paperspace Console:

1. Begin the Create Project flow and supply a Project name.
2. Run Experiments manually for the Project via the Experiment Builder or the CLI. See instructions on [installing the CLI](../get-started/install-the-cli.md), and instructions on how to [run an experiment from the CLI]().

**GradientCI Projects** allow you to run Experiments automatically simply by pushing code to a GitHub repository. See [GradientCI](gradientci.md) for information on setting up our continuous integration service that will run a new experiment whenever:

1. a new commit is pushed to the linked repo's default branch;
2. a PR is opened against that default branch;
3. a commit is pushed to such a PR's branch.

