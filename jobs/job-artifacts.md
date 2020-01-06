# Job Artifacts

## About

Interact with any job artifacts available to either the current authenticated user or the team, if the user belongs to a team. The artifacts method has 3 sub commands - list, get & destroy. 

### Artifacts List

```text
gradient jobs artifacts list --size --link --files model.* JOB_ID
```

#### Parameters

| ParameterName          | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `-s,--size` | boolean | &lt;optional&gt; | Show the file Size |
| `-l,--links` | boolean | &lt;optional&gt; | Show the file URL |
| `--files` | string | &lt;optional&gt; | Filter to get only a given file. Can use \* as a wildcard. |
| JOB\_ID | string | required |  job id to list artifacts for |

### Artifacts Get

Get all of the artifacts associated with a job.

```text
$ gradient jobs artifacts get JOB_ID
```

#### Parameters

| ParameterName          | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| JOB\_ID | string | required |  job id to get artifacts for |

### Artifacts Destroy

Destroy all of the artifacts associated with a job.

```text
$ gradient jobs artifacts destroy JOB_ID
```

#### Parameters

| ParameterName          | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| JOB\_ID | string | required |  job id to destroy artifacts for |

