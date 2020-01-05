# Delete a Job

## About

Destroy the job with the given id. When this action is performed, the job is immediately stopped and marked for deletion. Access to the job is terminated immediately and billing for the job is prorated to the minute.

## Example Use

```text
$ gradient jobs destroy --jobId "j123abc"
```

### **Properties**

| Name | Type | Description |
| :--- | :--- | :--- |
| `jobId` | string | The id of the job to destroy |

