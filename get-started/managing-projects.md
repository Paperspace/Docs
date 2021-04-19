# Organizing Projects

A Gradient Project is a workspace for you or your team to run Workflows, store Models, and manage Deployments. Projects create an additional isolation layer of organization and control \(e.g. managing access\) within your team.  You can [create a project](managing-projects.md#create-a-project) in the web UI or the CLI.

## Create a Project

{% tabs %}
{% tab title="Web UI" %}
On the [Projects page](https://console.paperspace.com/projects), click _Create Project_.

![](../.gitbook/assets/image%20%2821%29.png)

Provide a name and then click _Create Project_.

![](../.gitbook/assets/image%20%2820%29.png)
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

## Managing access to a Project

To add other team members to a project, click any Project in the projects list to navigate to its Project details page and then click the Accessors tab:

![](../.gitbook/assets/accessors.png)

On the Accessors tab you will find a list of users who already have access to the Project. Add an Accessor by clicking the "Add Accessor" button on the right side of the page. Assign other team members to the Project by selecting their name in the drop-down and clicking on "Assign User":

![](../.gitbook/assets/assign-user8%20%281%29.png)

You can also remove members' access to a Project by clicking the "Remove Access" button next to the member's name.

{% hint style="info" %}
Note: Only existing team members will be displayed in the drop-down list. Only Team admins can add additional team members to this list.

Additionally, project access can only be controlled through the web console – Accessors cannot be added or removed through the Gradient CLI.
{% endhint %}

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

