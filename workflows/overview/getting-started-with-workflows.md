# Getting Started with Workflows

## Creating Gradient Workflows

{% hint style="info" %}
View the full CLI/SDK Docs for **Workflows** here [https://paperspace.github.io/gradient-cli/gradient.cli.html\#gradient-workflows](https://paperspace.github.io/gradient-cli/gradient.cli.html#gradient-workflows)
{% endhint %}

1. Make sure you have the latest version of the [Gradient CLI](../../get-started/core-concepts/install-the-cli.md)
2. Create a  [Gradient Project](../../get-started/managing-projects.md) and [grab your project ID](../../get-started/managing-projects.md#get-your-projects-id)
3. Create your first workflow using the Gradient CLI

```bash
gradient workflows create --name <MY_FIRST_WORKFLOW> --projectId <project-id>
```

## Running your first workflow run

Create a workflow spec yaml file \([View the full workflow yaml spec](workflow-spec.md)\). You will also need:

**`workflow-id`** : Grab this by running `gradient workflows list` in the CLI i.e. `7634c165-5034-4f49-95fa-005fc0e7970b`

**`cluster-id`** : Currently ****workflows require that you have a [Gradient Private Cluster.](../../gradient-private-cloud/about/setup/managed-installation.md) The cluster ID looks like this: `cla7rjbzz`

```bash
gradient workflows run  \
    --id <worklow-id> \ 
    --clusterId <cluster-id> \
    --path ./workflow.yaml 
```

## 

