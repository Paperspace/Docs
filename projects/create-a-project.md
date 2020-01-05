---
description: How to create Standalone or GradientCI Projects
---

# Create a Project via the GUI

## Create a Standalone Project

On the Projects page, click _Create Project_ and select _Create Standalone Project_.

Provide a name and then click _Create Project_.

![](../.gitbook/assets/screen-shot-2019-05-28-at-2.38.20-pm.png)

## Create a GradientCI Project

[GradientCI](gradientci.md) Projects allow you to connect a GitHub repository to your Project in order to automatically run experiments when you push new commits or open pull requests \(PRs\).

Visit [www.paperspace.com/console/projects](https://www.paperspace.com/console/projects), click _Create Project_, and select **Create GradientCI Project**. Make sure you have installed **GradientCI** on the target repository to which you'll link your Project.

![](../.gitbook/assets/screen-shot-2019-05-30-at-9.11.47-pm.png)

If you haven't yet connected your GitHub account, follow the prompts to grant access to your GitHub repositories and to your GradientCI App installation:

![](../.gitbook/assets/screen-shot-2019-05-28-at-3.59.49-pm.png)

Then, select the GitHub repo from the dropdown list:

![](../.gitbook/assets/image%20%2823%29.png)

## Get Your Project's ID

When using the CLI, or for collaboration or reference, it can be useful to specify a Project's ID.

Click any Project in the Projects List to navigate to its Project Details page, and then click the Project ID to copy the value to your clipboard:

![](../.gitbook/assets/project-id.gif)

From the CLI, you can also enter the following command:

```bash
gradient projects list
```

