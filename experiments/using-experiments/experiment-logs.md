# Experiment Logs

Log streaming is available in both the web UI and CLI.  It is also possible to stream logs using the SDK.  

{% tabs %}
{% tab title="Web UI" %}
Navigate to a Job run part of an Experiment to view its logs.  These logs are streamed in realtime while the Experiment runs.  There are a few options such as Search, View all Logs, and Download Logs available on the page.  

![](../../.gitbook/assets/image%20%2832%29.png)
{% endtab %}

{% tab title="CLI" %}
You can stream logs while the Experiment is running or after it has stopped.‌

### Example Use

```bash
gradient experiments logs --experimentId <id>
```

### ‌Example Output

```text
Hello Paperspace
Creating file /artifacts/myoutput1.txt
Creating file /artifacts/myoutput2.txt
Finished; returning exit code 0
```

‌**Properties**

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `experimentId` | string | Required | Id of the experiment to view logs for. |
| `follow` | string | &lt;optional&gt; | ​Content |
| `line` | number | &lt;optional&gt; | Optional; if line is specified logs only logs after that line will be returned \(up to limit\). |
| `limit` | number | &lt;optional&gt; | Optional; number of log lines to retrieve on each request; default limit is 2000. |
{% endtab %}

{% tab title="SDK" %}
While using the SDK, you can print the logs of an Experiment.

```python
#create a log stream & print all logs for the duration of experiment
log_stream = experiment_client.yield_logs(experiment_id)
print("Streaming logs of experiment")
try:
    while True:
        print(log_stream.send(None))
except:
    print("done streaming logs")
```
{% endtab %}
{% endtabs %}

