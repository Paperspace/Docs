# Job Logs

Stream the logs for the job with the given id, while the job is running or after it has stopped.

## Example Use

```text
$ gradient jobs logs --jobId "j123abc"
```

### Example Output

```text
Hello Paperspace
Creating file /artifacts/myoutput1.txt
Creating file /artifacts/myoutput2.txt
Finished; returning exit code 0
```

### **Properties**

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `jobId` | string |  | Id of the job to logs |
| `tail` | boolean | &lt;optional&gt; | Optional; if tail is specified logs will be streamed until the job stops. |
| `line` | number | &lt;optional&gt; | Optional; if line is specified logs only logs after that line will be returned \(up to limit\). |
| `limit` | number | &lt;optional&gt; | Optional; number of log lines to retrieve on each request; default limit is 2000. |
| `json` | boolean | &lt;optional&gt; | Optional; return JSON object instead of writing to standard out. '--json' with no value is equivalent to true. |

