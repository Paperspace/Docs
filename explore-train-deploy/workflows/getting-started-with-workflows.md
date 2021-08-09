# Creating and Running Workflows

The following sections cover creating and running workflows, and authoring new workflow yaml specs.  If you have never run a workflow before check out the Workflows [quick-start](https://docs.paperspace.com/gradient/get-started/quick-start#advanced-mlops) then return here for more details.

## Creating Gradient Workflows

{% hint style="info" %}
View the full CLI/SDK Docs for **Workflows** here [https://paperspace.github.io/gradient-cli/gradient.cli.html\#gradient-workflows](https://paperspace.github.io/gradient-cli/gradient.cli.html#gradient-workflows)
{% endhint %}

1. Make sure you have the latest version of the [Gradient CLI](../../get-started/quick-start/install-the-cli.md)
2. Create a [Gradient Project](../../get-started/managing-projects/) and [grab your project ID](../../get-started/managing-projects/#get-your-projects-id)
3. Create your first workflow using the Gradient CLI

```bash
gradient workflows create --name <MY_FIRST_WORKFLOW> --projectId <project-id>
```

## Running your first workflow run

Create a workflow spec yaml file \([View the full workflow yaml spec](workflow-spec.md)\). You will also need:

**`workflow-id`** : Grab this by running `gradient workflows list` in the CLI, i.e., `7634c165-5034-4f49-95fa-005fc0e7970b`

```bash
gradient workflows run  \
    --id <worklow-id> \ 
    --path ./workflow.yaml
```

The next sections cover the syntax and concepts behind authoring new workflow yaml specs for MLops applications.
