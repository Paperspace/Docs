# Deployment Logs

Deployment logs are available in both the web UI and CLI. Logs are streamed in realtime during provisioning, runtime, and teardown, and are available as static values after the deployment is stopped.  

{% tabs %}
{% tab title="Web UI" %}
To view the Deployment logs, navigate to the Logs tab of the Deployment.

![](../../.gitbook/assets/image%20%2895%29.png)
{% endtab %}

{% tab title="CLI" %}
#### Syntax

```bash
gradient deployments logs --id <deployment> [OPTIONS]
```

#### Parameters

```text
Usage: gradient deployments logs [OPTIONS]

  List deployment logs

Options:
  --id TEXT                 [required]
  --line INTEGER
  --limit INTEGER
  --follow TEXT
  --apiKey TEXT             API key to use this time only
  --optionsFile PATH        Path to YAML file with predefined options
  --createOptionsFile PATH  Generate template options file
  --help                    Show this message and exit.
```
{% endtab %}
{% endtabs %}

