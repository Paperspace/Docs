# List your Jobs

## About

List information about all jobs available to either the current authenticated user or the team, if the user belongs to a team. The list method takes an optional first argument to limit the returned job objects.

## Example Use

```text
$ gradient jobs list --project "MyProject" --state Running --summary
```

### Parameters

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| `project` | string | &lt;optional&gt; | Optional project to match on. If neither project nor projectId are provided, this is taken from the .ps\_project/config.json file, or the current directory name. Specify 'all' to list jobs for all projects associated with the user or team if the user is on a team. |
| `projectId` | string | &lt;optional&gt; | Optional projectId to match on |
| `experimentId` | string | &lt;optional&gt; | Optional container to match on |
