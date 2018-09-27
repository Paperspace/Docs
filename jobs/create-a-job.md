# Create a Job

## About

Create a new Paperspace job, and tail its log output. To disable the tailing behavior specify `--tail false`. 

{% hint style="info" %}
**Note:** if a project is not defined for the current working directory, and you are running in command line mode, a project configuration settings file will be created. Use `--init false` or specify `--project [projectname]` to override this behavior.
{% endhint %}

## Run a Job

```text
$ paperspace jobs create <namespace> <command> [options...]
```

### Job Parameters

* Machine Type: Such as `--P100` or `--C7` or `--TPU`
* Container: Such as 

## Example

```text
$ paperspace jobs create \
    --container "http://dockerhub.com/mycontainer" \
    --machineType "P5000"
```



