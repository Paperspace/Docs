# Secrets

### Managing and Using Secrets

Secrets allow you to store sensitive information at the team, private cluster, and project level. The secrets you create are available to use in experiments run on private clusters.

Secrets can be created at the following levels:

* Team: these secrets are applied to all projects and all clusters
* Project: these secrets are applied to all experiments in a project
* Cluster: these secrets are applied to all experiments in a cluster

Secrets can be set from the Settings tab in the web UI or through the CLI.

{% hint style="info" %}
View the full CLI/SDK Docs for **Secrets** here [https://paperspace.github.io/gradient-cli/gradient.cli.html\#gradient-secrets](https://paperspace.github.io/gradient-cli/gradient.cli.html#gradient-secrets)
{% endhint %}

#### Set a Secret

{% tabs %}
{% tab title="Web UI" %}
Navigate to the project, cluster, or team page and click the **Secrets** tab. Click the **Create Secret** button, enter the secret name and value, and click the **Create Secret** button to save.

![Secrets are located in Settings &amp;gt; Secrets](../../.gitbook/assets/screen-shot-2021-01-18-at-10.25.39-pm.png)
{% endtab %}

{% tab title="CLI" %}
Set team secret

```text
gradient secrets set team --name=<name> --value=<secret>
```

Set project secret

```text
gradient secrets set project --id=<project_id> --name=<name> --value=<secret>
```

Set cluster secret

```text
gradient secrets set cluster --id=<cluster_id> --name=<name> --value=<secret>
```
{% endtab %}
{% endtabs %}

#### List Secrets

{% tabs %}
{% tab title="Web UI" %}
Navigate to the project or team page and click the **Secrets** tab.

![Secrets are available in settings for projects and teams](../../.gitbook/assets/screen-shot-2021-01-18-at-10.28.24-pm.png)
{% endtab %}

{% tab title="CLI" %}
List team secrets

```text
gradient secrets list team
```

List project secrets

```text
gradient secrets list project --id=<project_id>
```

List cluster secrets

```text
gradient secrets list cluster --id=<cluster_id>
```
{% endtab %}
{% endtabs %}

#### Delete a Secret

{% tabs %}
{% tab title="Web UI" %}
Navigate to the project, cluster, or team page and click the **Secrets** tab. Click the **Delete** button and confirm the dialog.

![](../../.gitbook/assets/secret-delete.png)
{% endtab %}

{% tab title="CLI" %}
Delete team secret

```text
gradient secrets delete team --name=<name>
```

Delete project secret

```text
gradient secrets delete project --id=<project_id> --name=<name>
```

Delete cluster secrets

```text
gradient secrets delete cluster --id=<cluster_id> --name=<name>
```
{% endtab %}
{% endtabs %}

#### **Secret scoping**

If the same secret name is created for more than one scope only one will be applied. Secret with the same name have the following precedence: Cluster secrets take precedence over Team secrets; Project secrets take precedence over both Cluster secrets and Team secrets.

