# View Machine Types

Return a list of available cluster machine types. If the isBusy property is true then all machines of the specified type and cluster are currently running jobs. The machineTypes method takes an optional first argument to limit the returned cluster machine type objects.

## Example Use

```text
$ paperspace jobs machineTypes
```

### Example Return Value

```text
[
  {
    "region": "East Coast (NY2)",
    "cluster": "PS Jobs",
    "machineType": "P5000",
    "isBusy": false,
  },
  {
    "region": "East Coast (NY2)",
    "cluster": "PS Jobs",
    "machineType": "V100",
    "isBusy": false,
  },
  {
    "region": "GCP West",
    "cluster": "PS Jobs on GCP",
    "machineType": "K80",
    "isBusy": false,
  },
  {
    "region": "GCP West",
    "cluster": "PS Jobs on GCP",
    "machineType": "P100",
    "isBusy": false,
  }
]
```

### **Properties**

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `region` | string | &lt;optional&gt; | Optional region to match on |
| `cluster` | string | &lt;optional&gt; | Optional cluster to match on |
| `machineType` | string | &lt;optional&gt; | Optional machine type to macth on |
| `isBusy` | boolean | &lt;optional&gt; | Optional busy status value to match on |

