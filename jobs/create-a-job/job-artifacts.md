# Job Artifacts

{% hint style="warning" %}
This feature is only available in the hosted gradient Gradient version. [Contact Sales](https://info.paperspace.com/contact-sales) to learn more.
{% endhint %}

## About

Interact with any job artifacts available to either the current authenticated user or the team, if the user belongs to a team. The artifacts method has 3 sub commands - list, get & destroy. 

### Artifacts List

```bash
gradient jobs artifacts list --size --link --files model.* <job id>
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

```bash
gradient jobs artifacts get <job id>
```

#### Parameters

| ParameterName          | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| JOB\_ID | string | required |  job id to get artifacts for |

### Artifacts Destroy

Destroy all of the artifacts associated with a job.

```bash
gradient jobs artifacts destroy <job id>
```

#### Parameters

| ParameterName          | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| JOB\_ID | string | required |  job id to destroy artifacts for |

