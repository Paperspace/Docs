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

### Job Parameters Summary

* Machine Type: Such as `--P100` or `--C7` or `--TPU`
* Container: Such as `--tensorflow/tensorflow:1.5.1-gpu`
* Command: Such as `"./do.sh"`

### Example

```
$ paperspace jobs create \
    --container "http://dockerhub.com/mycontainer" \
    --machineType "P5000" \
    --command "/paperspace/run.sh" 
```

### Job Parameters Complete List

**Properties**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Attributes</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>container</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A required reference to a docker image in a public or private docker registry,
        or a container name provided by Paperspace. Docker image repository references
        must be in lowercase and may include a tag and a hostname prefix followed
        by a slash; if committed the hostname defaults to that of the public Docker
        Hub registry. An example docker image reference: <code>docker.io/mynamespace/myimage:mytag</code>.
        A container name may be mixed case. (Designated container names are currently
        only provided as part of various Gradient tutorials and samples.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>machineType</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
          <br />
      </td>
      <td style="text-align:left">
        <p>An optional machine type to run the job on: either 'GPU+', 'P4000', 'P5000',
          'P6000', 'V100', 'K80', 'P100', or 'TPU'.</p>
        <p>Defaults to 'K80'.</p>
        <p>Note: the 'K80', 'P100', and 'TPU' machineTypes run on Google Cloud Platform
          (GCP). The other machineTypes run on the Paperspace Cloud. Google Cloud
          platform and Paperspace Cloud have distinct Job Storage spaces; Job storage
          is not currently shared between these two cloud environments.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>name</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional name or description for this job. If committed, the job name
        defaults to 'job N' where N represents the Nth job instance for the given
        project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>project</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">The name of the project for this job. If not provided, this is taken from
        the .ps_project/config.json file, or the current directory name.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>projectId</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
          <br />
      </td>
      <td style="text-align:left">The project id of an existing project for this job. Note: if projectId
        is specified, the project parameter cannot be specified.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>command</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional command to run within the workspace or container.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspace</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional path to a workspace, or link to a git repository to upload
        and merge with the container. If a zip file name is provided it is uploaded
        instead. If no workspace is provided the current directory is zipped up
        and transferred. If the workspace is 'none', no workspace is merged and
        the container is run as-is. To download a git repository provide an https
        repository link and optionally prefix it with 'git+', e.g. 'https://github.com/MyProjects/MyRepo.git'.
        If the 'git+' prefix is not specified, it is added at the time of download
        to the job runner machine. S3 links are also supported using the schema
        's3://bucketname/objectname'.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>dataset</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional reference to a dataset to be merged with the container.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>registryUsername</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional username for accessing an image hosted on a private container
        registry. Note: you must specify this option every time a private image
        is specified for the container.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>registryPassword</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional password for accessing an image hosted on a private container
        registry. Note: you must specify this option every time a private image
        is specified for the container.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceUsername</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional username for accessing a private git repository. Note: you
        must specify this option every time a private git repository is specified
        for the workspace.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspacePassword</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional password for accessing a private git repository. We recommend
        using an OAuth token (GitHub instructions can be found <a href="https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/">here</a>).
        Note: you must specify this option every time a private git repository
        is specified for the workspace.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ports</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">An optional list of port mappings to open on the job cluster machine while
        the job is running. The port mappings are specified as 'XXXX:YYYY' where
        XXXX is an external port number and YYYY is an internal port number. Multiple
        port mappings can be provided as a comma separated list. Port numbers must
        be greater than 1023. Note: only /tcp protocol usage is supported.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>tail</code>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">Optional; defaults to true in command line mode only. Specify false to
        disable automatic tailing.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>json</code>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <optional>
      </td>
      <td style="text-align:left">Optional; if true, do not write progress to standard out. <code>--json</code>with
        no value is equivalent to true.</td>
    </tr>
  </tbody>
</table>

