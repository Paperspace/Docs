# Using Tags

## Adding, Creating, Removing, and Filtering by Tag

### Adding Tags to Entities

Team admins can add new and existing tags to any of their team's entities. Team members can add new and existing tags to entities that they created. Any new tag will become available for use across all of a team's entities.

{% tabs %}
{% tab title="Web UI" %}
To add, create, or remove a tag on any taggable entity, click the **Tag** button. This will open the **Edit Tags** modal, where you can: 1\) see any current tags on that entity, 2\) create and add new tags, and 3\) remove current tags. After you've added or removed tags, click **Submit** to finalize your changes.

![Adding tags to a project -- one new and one existing](../.gitbook/assets/tagging-entity-add.gif)

![Removing tags from a project](../.gitbook/assets/tagging-entity-remove.gif)
{% endtab %}

{% tab title="CLI" %}
The Gradient CLI enables you to add tags manually for experiments, projects, deployments and notebooks.

To add a tag to a given entity all you need to do is:

`gradient <entity> tags add <entity id> --tags "tag1, tag2"`

For example to add multiple tag to deployments:

```text
gradient deployments tags add <deployment id> --tags "tag1,tag2"
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Note that you can use the `--help` option at any time to reveal information in your terminal about the current command you wish to use. Alternately, if you simply try to run a command, the CLI will prompt you for additional subcommands that you may be intending to use, as well as required options that are missing from your command.
{% endhint %}

### Filtering Entities by Tag

{% tabs %}
{% tab title="Web UI" %}
To find entities with a specific tag, first click the **Filter by tags** dropdown at the top of any entity list. The example below uses Projects.

![Filter by tags dropdown where you can select tags to filter on](../.gitbook/assets/screen-shot-2020-02-10-at-7.59.50-pm.png)

Type or select tags to filter the entity. This will result in all entities that match the selected tags.

![Project results that match the tag in question](../.gitbook/assets/screen-shot-2020-02-10-at-7.25.47-pm%20%281%29%20%281%29.png)

You can also add tags to filter the current entity list by clicking on any tag on any entity.
{% endtab %}

{% tab title="CLI" %}
To filter for example experiments by tags: 

`gradient experiments list [OPTIONS] --tag 'TAG'`

You can use --tags multiple times:

`gradient experiments list [OPTIONS] --tag 'TAG1' --tag 'TAG2'`
{% endtab %}
{% endtabs %}



