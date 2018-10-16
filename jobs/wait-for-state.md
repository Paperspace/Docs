# Wait for State

## About

Wait for the job with the given id to enter a certain job state. This action polls the server and returns only when we detect that the job has transitioned into the given state, or to the 'Error' state. 

## States

States available to query for are:

* `Pending`- the job has not started setting up on a machine yet
* `Running` - the job is setting up on a machine, running, or tearing down
* `Stopped` - the job finished with a job command exit code of 0
* `Error` - the job was unable to setup or run to normal completion
* `Failed` - the job finished but the job command exit code was non-zero
* `Cancelled` - the job was manual stopped before completion

When the callback is called, the returned object will be information about the job.

## Example Use

```text
$ paperspace jobs waitfor \
    --jobId "j123abc" \
    --state "Stopped"
```

### Properties

| Name | Type | Description |
| :--- | :--- | :--- |
| `jobId` | string | Id of the job to wait for |
| `state` | string | Name of the state to wait for |

