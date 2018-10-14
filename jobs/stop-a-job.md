# Stop a Job

## About

Stop an individual job. If the job is already stopped, this action is a no-op. If the job is running, it will be stopped.

**Properties**

| Name | Type | Description |
| :--- | :--- | :--- |
| `jobId` | string | The id of the job to shut down |

## Example

```text
$ paperspace jobs stop --jobId "j123abc"
```

