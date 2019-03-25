# Create a Project

## Create a Project

### About

As of 7.0, a Gradient Project is a creative workspace for a team or user to run Experiments. Projects can be powered by GradientCI \(via GitHub\), or they can be "Standalone."

**GradientCI Projects** allow you to run Experiments automatically simply by pushing code to a GitHub repository. See [GradientCI](gradientci.md) for information on setting up our continuous integration service that will run a new experiment whenever:

1. a new commit is pushed to the linked repo's default branch;
2. a PR is opened against that default branch;
3. a commit is pushed to such a PR's branch.

**Standalone Projects** require you to provide the code and run new Experiments manually, just like running Jobs prior to 7.0. To create a standalone Project via the Paperspace Console:

1. Begin the Create Project flow and supply a Project name.
2. Run Experiments manually for the Project via the Experiment Builder or the CLI. See instructions on [installing the CLI](../cli/install-the-cli.md), and instructions on how to [run an experiment from the CLI](../cli/run-experiments.md).

