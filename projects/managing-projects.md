# Managing Projects

## Create a Standalone Project

{% tabs %}
{% tab title="Web UI" %}
On the Projects page, click _Create Project_ and select _Create Standalone Project_.

![](../.gitbook/assets/image%20%2857%29.png)

Provide a name and then click _Create Project_.

![](../.gitbook/assets/image%20%2844%29.png)
{% endtab %}

{% tab title="CLI" %}
The following command creates a Project called `ExampleProject` 

```
gradient projects create --name ExampleProject [OPTIONS]
```

#### Parameters: 

| Option | Description |
| :--- | :--- |
| `--name` | Name of new project \[required\] |
| `--repositoryName` | Name of the repository |
| `--repositoryUrl` | URL to the repository |
| `--apiKey` | Key to use this time only |
| `--help`  | Help for this feature |
{% endtab %}
{% endtabs %}

## Create a GradientCI Project

{% tabs %}
{% tab title="Web UI" %}
[GradientCI](gradientci.md) Projects allow you to connect a GitHub repository to your Project in order to automatically run experiments when you push new commits or open pull requests \(PRs\).

Visit [www.paperspace.com/console/projects](https://www.paperspace.com/console/projects), click _Create Project_, and select **Create GradientCI Project**. Make sure you have installed **GradientCI** on the target repository to which you'll link your Project.

![](../.gitbook/assets/screen-shot-2019-05-30-at-9.11.47-pm.png)

If you haven't yet connected your GitHub account, follow the prompts to grant access to your GitHub repositories and to your GradientCI App installation:

![](../.gitbook/assets/screen-shot-2019-05-28-at-3.59.49-pm.png)

Then, select the GitHub repo from the dropdown list:

![](../.gitbook/assets/image%20%2830%29.png)
{% endtab %}

{% tab title="CLI" %}
[GradientCI](gradientci.md) Projects allow you to connect a GitHub repository to your Project in order to automatically run experiments when you push new commits or open pull requests \(PRs\).

Make sure you have installed **GradientCI** on the target repository to which you'll link your Project.

{% hint style="info" %}
The following command creates a Project called `ExampleProject` 
{% endhint %}

```bash
gradient projects create --name ExampleProject --repositoryName <name> --repositoryUrl <url>
```

#### Parameters: 

| Option | Description |
| :--- | :--- |
| `--name` | Name of new project \[required\] |
| `--repositoryName` | Name of the repository |
| `--repositoryUrl` | URL to the repository |
| `--apiKey` | Key to use this time only |
| `--help`  | Help for this feature |
{% endtab %}
{% endtabs %}

## Get Your Project's ID

A Project's ID is a required parameter for several commands within Gradient.

{% tabs %}
{% tab title="Web UI" %}
To find the ID, click any Project in the Projects List to navigate to its Project Details page, and then click the Project ID to copy the value to your clipboard:

![](../.gitbook/assets/project-id.gif)
{% endtab %}

{% tab title="CLI" %}
To get a Project ID, you can use the following command:

```bash
gradient projects list
```
{% endtab %}
{% endtabs %}

## Deleting a Project

{% tabs %}
{% tab title="Web UI" %}
You can delete a project by visiting the project's `Settings` page and hitting the `Delete Project` button.  

![](../.gitbook/assets/project-settings.jpg)

![](../.gitbook/assets/deleteproject.jpg)
{% endtab %}

{% tab title="CLI" %}
To delete a Project, you can use the following command:

```bash
gradient projects delete --id <project id>
```
{% endtab %}
{% endtabs %}

