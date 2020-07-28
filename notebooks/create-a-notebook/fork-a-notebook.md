# Fork a Notebook

## Fork your Notebook

Forking is a great way to make a copy of your Notebook; to save a version of it that you may want to go back to in case you expect to make major changes.  Forking a notebook creates a new history for your notebook.  This can copy notebooks, including public notebooks, into a team.  

{% tabs %}
{% tab title="Web UI" %}
Click the Fork icon to the right of a notebook:

![](../../.gitbook/assets/image%20%2878%29.png)

You will see an exact copy of your notebook appear at the top of your Notebooks list.
{% endtab %}

{% tab title="CLI" %}
After the fork there will be a stopped notebook created in your team you must call `gradient notebooks start --id ID` to run it.

### Usage

```bash
gradient notebooks fork [OPTIONS]
```
{% endtab %}
{% endtabs %}



