# Create a Project

## Create a Project

### About

As of 7.0, a Gradient Project is a creative workspace for a team or user to run Experiments. Projects can be powered by GradientCI \(via GitHub\), or they can be "Standalone."

**GradientCI Projects** allow you to run Experiments automatically simply by pushing code to a GitHub repository.

**Standalone Projects** require you to provide the code and run new Experiments manually, just like running Jobs prior to 7.0.

### Creating a GradientCI Project via the Paperspace Console

To create a Gradient Project with continuous integration powered by GradientCI and GitHub:

1. Install the [GradientCI](https://github.com/apps/gradientci) GitHub app on your repository. \(GitHub Admin privilege is required.\)
2. Navigate to the [Projects page](https://www.paperspace.com/console/projects).
3. Click Create Project.
4. Select GitHub Project.
5. Grant Paperspace access to your GitHub repos via OAuth.
6. Confirm a repo with GradientCI installed for your new Gradient° Project.

Voilà! GradientCI will run a new experiment whenever:

1. a new commit is pushed to the linked repo's default branch;
2. a PR is opened against that default branch;
3. a commit is pushed to such a PR's branch.

### Creating a Standalone Paperspace Project via the Paperspace Console

1. Begin the Create Project flow and supply a Project name.
2. Run Experiments manually for the Project via the Experiment Builder or [the CLI](https://github.com/Paperspace/paperspace-python).

