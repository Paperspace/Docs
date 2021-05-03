# Using Jobs

{% hint style="warning" %}
This feature is currently only available to our Gradient Managed service. [Contact Sales](https://info.paperspace.com/contact-sales) to learn more. 
{% endhint %}

## Creating a Job

{% tabs %}
{% tab title="Web UI" %}
![](../../.gitbook/assets/image%20%2845%29.png)

Jobs can be submitted via the Job Builder.  There are a variety of optional and required options for your job including the instance type, the command, the container, etc.  Note: At the top of the screen, you'll see a few job presets which will give a sense for how these options work.  

* **Machine Type.** What type of instance to run your Job on. We recommend starting with a GPU+. Many Jobs benefit from a machine with a GPU, but some can run just using a CPU.
* **Container.** Jobs are run within a docker container. You can run a public or private container. Learn more [here](https://support.paperspace.com/hc/en-us/articles/360003415434). 
* **Workspace.** The workspace is the collection of code that is run. It can be a Git repository \(public or private\), your local working directory \(if you are using the CLI\) which is uploaded to the docker container during the job running process, or `none` \(default value\). 
* **Command.** The command is the entry point to the container. This is the line of code that will kick off your Job. It could be a bash script `./run.sh` or `python main.py` as just some examples. 
* **Custom Metrics.** Enter a list of custom metrics to use with Gradient's [statd client](job-metrics/custom-metrics.md), such as `percent_failure` or `percent_success`.

Once you have examined or specified the parameters, hit "Submit Job" and watch the Job run!

The Job Builder is great for getting started with basic tasks.  For more advanced workflows, we recommend using the CLI which offers more flexibility.
{% endtab %}

{% tab title="CLI" %}
### Syntax

```bash
gradient jobs create <namespace> <command> [options...]
```

### Job Parameters Basics

* Machine Type: Such as `--P100` or `--C7` or `--TPU`
* Container: Such as `--tensorflow/tensorflow:1.5.1-gpu`
* Command: Such as `"./do.sh"`

## Example Use

```bash
gradient jobs create \
    --name "my job" \
    --container "http://dockerhub.com/mycontainer" \
    --machineType "P5000" \
    --command "/paperspace/run.sh"
    --projectId "someProjectID"
```
{% endtab %}
{% endtabs %}

## Job Parameters Complete List

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>name</code>
      </td>
      <td style="text-align:left">[required]</td>
      <td style="text-align:left">Job name</td>
    </tr>
    <tr>
      <td style="text-align:left">projectId</td>
      <td style="text-align:left">[required]</td>
      <td style="text-align:left">Project ID</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>machineType</code>
      </td>
      <td style="text-align:left">K80</td>
      <td style="text-align:left">An optional machine type to run the job on: either &apos;GPU+&apos;, &apos;P4000&apos;,
        &apos;P5000&apos;, &apos;P6000&apos;, &apos;V100&apos;, &apos;K80&apos;,
        &apos;P100&apos;, or &apos;TPU&apos;.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>container</code>
      </td>
      <td style="text-align:left">paperspace/tensorflow-python</td>
      <td style="text-align:left">A reference to a docker image in a public or private docker registry,
        or a container name provided by Paperspace. Docker image repository references
        must be in lowercase and may include a tag and a hostname prefix followed
        by a slash; if committed the hostname defaults to that of the public Docker
        Hub registry. An example docker image reference: docker.io/mynamespace/myimage:mytag.
        A container name may be mixed case. (Designated container names are currently
        only provided as part of various Gradient tutorials and samples.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>command</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Job command/entrypoint</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspace</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Path to workspace directory. (Soon also will support a path to a workspace
        archive or git repository URL.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceArchive</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Path to workspace archive. (Currently being deprecated in an upcoming
        version.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceUrl</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Project git repository URL. (Currently being deprecated in an upcoming
        version.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workingDirectory</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Working directory for the experiment</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>experimentId</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Experiment Id</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>jobEnv</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Environmental variables in JSON String Format. Example:</p>
        <p>{ &quot;HKS_EPOCHS&quot;: 1, &quot;HKS_MAX_EVALS&quot;: 4, &quot;DATASET_SIZE&quot;:
          10000 }</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>project</code>
      </td>
      <td style="text-align:left">$CWD</td>
      <td style="text-align:left">The name of the project for this job. If not provided, this is taken from
        the .ps_project/config.json file, or the current directory name.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>apiKey</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">API key to use this time only</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ignoreFiles</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Ignore certain files from uploading</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
Environment variables are available for use within the context of your job. The following host config options are currently exposed within the container:

`$PS_HOST_PUBLIC_IP_ADDRESS` - the public IP address of the host machine running the job

`$PS_HOST_PRIVATE_IP_ADDRESS` - the private IP address of the host machine running the job

`$PS_HOSTNAME` - the hostname of the host machine running the job

These can be used in conjunction with the `ports` option to send HTTP traffic to the job while it's in progress for example.
{% endhint %}

