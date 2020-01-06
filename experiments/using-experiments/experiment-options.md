# Experiment options

{% tabs %}
{% tab title="Web UI" %}
## Experiment web UI Options List

| Option | Description |
| :--- | :--- |
| **Machine Type** | This is the type of instance to run your Experiment's on. Many Experiments benefit from a machine with a GPU, but some can run just using a CPU. |
| **Container** | Experiments are run within a docker container. You can run a public or private container. Learn more [here](../containers-public-and-private.md).  |
| **Workspace** | The workspace is the collection of code that is run. The options in the web UI are a Git repo \(eg [https://github.com/Paperspace/fast-style-transfer.git](https://github.com/Paperspace/fast-style-transfer.git)\) or _none_.  The CLI offers more advanced options such as specifying a local directory, private Git repos, S3 buckets, and more. |
| **Command** | The command is the entry point to the container. This is the line of code that will kick off your experiment's job. It could be a bash script `./run.sh` or `python main.py` as a few examples.  |
| **Ports** | You have the option to attach a public IP automatically. Supports opening multiple ports simultaneously, separated by `:` . Learn more about opening ports [here](ports.md).  |
| **Custom Metrics** | Enter a list of custom metrics to use with Gradient's statd client, such as percent\_failure or percent\_success. |
{% endtab %}

{% tab title="CLI" %}
## Experiment CLI Options List

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>name</code>
      </td>
      <td style="text-align:left">Experiment name</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ports</code>
      </td>
      <td style="text-align:left">An optional list of port mappings to open on the instance while the job
        is running. The port mappings are specified as &apos;XXXX:YYYY&apos; where
        XXXX is an external port number and YYYY is an internal port number. Multiple
        port mappings can be provided as a comma separated list. Port numbers must
        be greater than 1023. Note: only /tcp protocol usage is supported. Learn
        more <a href="ports.md">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspace</code>
      </td>
      <td style="text-align:left">Path to workspace directory. (Soon also will support a path to a workspace
        archive or git repository URL.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceRef</code>
      </td>
      <td style="text-align:left">An option to specify a Git commit hash, branch name or tag. Learn more
        <a
        href="git-commit-tracking.md">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceArchive</code>
      </td>
      <td style="text-align:left">Path to workspace archive. (Currently being deprecated in an upcoming
        version.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceUrl</code>
      </td>
      <td style="text-align:left">Path to workspace archive. (Currently being deprecated in an upcoming
        version.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspaceUsername</code>
      </td>
      <td style="text-align:left">Used to pass-in a username to a private repo.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workspacePassword</code>
      </td>
      <td style="text-align:left">Used to pass-in a password to a private repo.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ignoreFiles</code>
      </td>
      <td style="text-align:left">When using the directory upload option, this command can be used to ignore
        certain files from uploading.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>workingDirectory</code>
      </td>
      <td style="text-align:left">Working directory for the experiment</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>artifactDirectory</code>
      </td>
      <td style="text-align:left">Where artifacts can be located.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clusterId</code>
      </td>
      <td style="text-align:left">Cluster ID of the private Gradient cluster. Learn more <a href="../../gradient-private-cloud/about.md">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>experimentEnv</code>
      </td>
      <td style="text-align:left">
        <p>Environmental variables in JSON String Format. Example:</p>
        <p><code>{&quot;HKS_EPOCHS&quot;:1,&quot;HKS_MAX_EVALS&quot;:4,&quot;DATASET_SIZE&quot;:100}</code> Learn
          more <a href="environment-variables.md">here</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>projectId</code>
      </td>
      <td style="text-align:left">Your <a href="../../projects/managing-projects.md#get-your-projects-id">Project ID</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>modelType</code>
      </td>
      <td style="text-align:left">This option is used to specify the format of your model. Learn more
        <a
        href="../../models/create-a-model/model-path.md">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>modelPath</code>
      </td>
      <td style="text-align:left">This option is used to locate your model. Learn more <a href="../../models/create-a-model/model-path.md">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>isPreemptible</code>
      </td>
      <td style="text-align:left">Flag that specifies if the Experiment is <a href="../../instances/preemptible-instances.md">preemptible</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>container</code>
      </td>
      <td style="text-align:left">A reference to a docker image in a public or private docker registry,
        or a container name provided by Paperspace. Docker image repository references
        must be in lowercase and may include a tag and a hostname prefix followed
        by a slash; if committed the hostname defaults to that of the public Docker
        Hub registry. An example docker image reference: docker.io/mynamespace/myimage:mytag.
        A container name may be mixed case. (Designated container names are currently
        only provided as part of various Gradient tutorials and samples.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>machineType</code>
      </td>
      <td style="text-align:left">An optional machine type to run the job on: either &apos;GPU+&apos;, &apos;P4000&apos;,
        &apos;P5000&apos;, &apos;P6000&apos;, &apos;V100&apos;, &apos;K80&apos;,
        &apos;P100&apos;, or &apos;TPU&apos;.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>command</code>
      </td>
      <td style="text-align:left">Experiment entrypoint command.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>containerUser</code>
      </td>
      <td style="text-align:left">Name of user in container.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>registryUsername</code>
      </td>
      <td style="text-align:left">Used to pass-in a username to a private container registry.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>registryPassword</code>
      </td>
      <td style="text-align:left">Used to pass-in a password to a private container registry.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>registryUrl</code>
      </td>
      <td style="text-align:left">Used to pass-in a path to a container in private container registry.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>no-logs</code>
      </td>
      <td style="text-align:left">Flag to prevent streaming logs in terminal.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>datasetUri</code>
      </td>
      <td style="text-align:left">Url to S3 bucket with dataset</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>datasetName</code>
      </td>
      <td style="text-align:left">Name of dataset</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>datasetAwsAccessKeyId</code>
      </td>
      <td style="text-align:left">S3 bucket&apos;s Access Key ID</td>
    </tr>
    <tr>
      <td style="text-align:left">datasetAwsSecretAccessKey</td>
      <td style="text-align:left">S3 bucket&apos;s Secret Access Key</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>datasetVersionId</code>
      </td>
      <td style="text-align:left">S3 dataset&apos;s version ID</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>datasetEtag</code>
      </td>
      <td style="text-align:left">S3 dataset&apos;s ETag</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>tensorboard</code>
      </td>
      <td style="text-align:left">Add to existing <a href="../../tensorboards/about.md">TensorBoard</a>.
        If no or many
        <br />TensorBoard exists a new one will be created.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>apiKey</code>
      </td>
      <td style="text-align:left">API key to use this time only.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>optionsFile</code>
      </td>
      <td style="text-align:left">Path to <a href="gradient-config.yaml.md">YAML file</a> with predefined
        options.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>createOptionsFile</code>
      </td>
      <td style="text-align:left">Generate template options file</td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}

