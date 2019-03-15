# Create a Gradientº Project

## About

As of 7.0, a Gradientº Project is a creative workspace for a team or user to run Experiments.

Projects can be powered by GradientCI (via GitHub), or alternatively they can be "Standalone".

GradientCI Projects allow you to automatically run experiments simply based on pushing code to a GitHub repository.

Standalone Projects require you to provide the code and run new experiments manually, just like running Jobs prior to 7.0.

## Creating a GradientCI Project via the Paperspace Console

To create a Gradient° Project with continuous integration powered by GradientCI and GitHub:</p>

1. Install the [GradientCI](https://github.com/apps/gradientci) GitHub app on your repository. (GitHub Admin privilege is required.)
1. Navigate to the [Projects page](https://www.paperspace.com/console/projects).
1. Click Create Project.
1. Select GitHub Project.
1. Grant Paperspace access to your GitHub repos via OAuth.
1. Confirm a repo with GradientCI installed for your new Gradient° Project.

Voilà! GradientCI will run a new experiment whenever:
1. a new commit is pushed to the linked repo's default branch;
1. a PR is opened against that default branch;
1. a commit is pushed to such a PR's branch.

## Creating a Standalone Paperspace Project via the Paperspace Console
1. Begin the Create Project flow and supply a project name.
1. Run experiments manually for the Project via the Experiment Builder or [the CLI](https://github.com/Paperspace/paperspace-python).

# Create a pre-7.0 Project

Prior to 7.0, a project was simply a directory or name for a set of related files and jobs. 

## Initializing a New Project via the CLI

If you do not initialize a particular name or directory, job commands will be given a project name corresponding to the current directory name. 

```
$ paperspace project init
```

This creates a `.ps_project/config.yaml` file in the current directory to cache information about the project, such as the name, or the last job created.
