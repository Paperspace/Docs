# Show Job info

## About

Show job information for the job with the given id.

**Properties**

| Name | Type | Description |
| :--- | :--- | :--- |
| `jobId` | string | Id of the job to show |

## Example

```text
$ paperspace jobs show --jobId "j123abc"
```

### Example return value

```text
{
  "id": "j123abc",
  "name": "job for project myproject",
  "state": "Running",
  "workspaceUrl": "myproject.zip",
  "workingDirectory": "/paperspace",
  "artifactsDirectory": "/artifacts",
  "entrypoint": "echo Hello Paperspace",
  "projectId": "pr456def",
  "project": "myproject",
  "container": "http://dockerhub.com/mycontainer",
  "machineType": "P5000",
  "cluster": "PS Jobs",
  "usageRate": "P5000 hourly",
  "startedByUserId": "u789ghi",
  "parentJobId": null,
  "jobError": null,
  "dtCreated": "2017-11-30T18:46:10.394Z",
  "dtModified": "2017-11-30T18:46:10.394Z",
  "dtProvisioningStarted": "2017-11-30T18:46:50.467Z",
  "dtProvisioningFinished": "2017-11-30T18:47:12.508Z",
  "dtStarted": "2017-11-30T18:47:14.636Z",
  "dtFinished": null,
  "dtTeardownStarted": null,
  "dtTeardownFinished": null,
  "dtDeleted": null,
  "exitCode": null
}
```

