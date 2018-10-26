# Usage

## **Usage of gradient-node**

```text
$ gradient-node [--apiKey ] [--name ] [--id ] [--cluster ] [--clusterId ] [--logHost ]
```

`--apiHost string` Gradient API Host \(default "[https://gradient-api.paperspace.io](https://gradient-api.paperspace.io)"\).

`--apiKey string` Paperspace api key value.

`--cluster string` Cluster Name for this node. If no cluster with this name exists a new one will be created.

`--clusterId string` Cluster ID for this node, e.g. "cXXXXXXXX". Takes precedence over the Cluster Name option if both are specified.

`--debug` Debug mode.

`--id string` Node ID, e.g. "cmXXXXXXXXXXXXXX". If specified with the Node Name option, the node name will be updated.

`--logHost string` Gradient Log Host \(default "[https://logs.paperspace.io](https://logs.paperspace.io)"\).

`--name string` Node Name; defaults to the current hostname. Specify with the --id  option to changed the name of an existing node.

`--mount string` Used for mapping one or multiple user mounted volumes to the docker container running the job. 

Optional ENVIRONMENT VARIABLES: 

{% hint style="info" %}
These can be used to configure the options above via environment settings. Note that any command line options take precedence over the environment settings.
{% endhint %}

```text
GRADIENT_NODE_API_KEY=<key> 
GRADIENT_NODE_NAME=<name> 
GRADIENT_NODE_ID=<id> 
GRADIENT_NODE_CLUSTER=<cluster_name> 
GRADIENT_NODE_CLUSTERID=<cluster_id> 
GRADIENT_NODE_API_HOST=<api_host_url> 
GRADIENT_NODE_LOG_HOST=<log_host_url> 
GRADIENT_NODE_DEBUG=[‘true’|’false’]
```

## **Root privileges**

Gradient-node needs to run with root privileges in order to communicate with docker on the host machine.  Therefore, if you are not running under a root account, you need to invoke gradient-node using sudo, e.g.:

```text
sudo ./gradient-node --apiKey XXXXXXXXXXXXXXXX
```

Note: sudo access is required even if you set up docker not to require sudo

## **Required Parameters**

The `--apiKey <key>` option is the only required parameter. It may also be provided via an environment variable, `GRADIENT_NODE_API_KEY=<key>`.
The API key can also be passed in at runtime by placing it in the `~/.paperspace/config.json` file on your local machine running gradient-node. The config.json format should be as follows:
```
{
  "apiKey": "ps6a...393",
  "name": "my-api-key-name"
}
```

## Naming and Registration

On startup gradient-node will attempt to register in the account associated with the provided api key, using a default or provided node name, and return a unique id for the name. By default it will use the local hostname as the name of the instance. Each time gradient-node is run with a unique name a new cluster machine entry with a unique id is created unless a node id is also provided. The `--name` option can be used to override the default name.

If a gradient-node instance with the same name already exists within the cluster then all running nodes with the same name will be eligible to run jobs. The Gradient web UI ****will only show one entry for each distinct node id however.

If you run gradient-node on a second machine, either make sure the second machine has a distinct hostname, or provide the `--cluster`  option with a distinct name. If you want the new instance to take over for an existing instance with the same name then you must stop any other currently running instances registered with that name. You can use the Gradient web UI to check for active running instances with that name.

If you want to change the name of a gradient-node instance you can specify the `--id`  option, along with the new name using the `--name`  option. This will update the name associated with that gradient-node id.

## Specifying a Cluster

Each gradient-node instance is part of a unique private cluster within the user’s account. When starting gradient-node you can specify the cluster to register in using the `--cluster <name>`  or the `--clusterId <cluster_id>`  option. However if both are provided, the `--clusterId <cluster_id>`  option takes precedence.

If no cluster name or cluster id is specified when running gradient-node the instance is registered in the user account’s default cluster. The initial name for this cluster is “GradientNode Cluster”.

If you are a registering gradient-node for the first time in your account, you can pick a different name for the default cluster using the `--cluster <cluster_name>`  option. On subsequent runs you can omit the cluster name option if you want to register the gradient-node instance in the same default cluster.

After the first cluster is created, if you register a node specifying a different cluster name, then a new cluster with that new name will automatically be created. However, it will not be the default cluster for the account.

In the Gradient web UI you can change the cluster name for any cluster in your account and/or switch which cluster is currently the default. When scheduling jobs you can select the targeted cluster using the paperspace CLI or API job create options.

## Example Output on Startup

The following shows a sample of log messages generated when starting and registering gradient-node. The `name`, `id`, `cluster`, and `cluserId` parameters are displayed, along with the node attributes structure, `nodeAttrs`, which is described below.

```text
2018/10/09 19:53:48 Starting gradient-node 6.7 ba95b2d 2018-10-09_18:12:45_UTC
2018/10/09 19:53:49 GradientNode name: ubuntu
2018/10/09 19:53:49 GradientNode id: cmdc2sjlenkhwx
2018/10/09 19:53:49 GradientNode cluster: GradientNode Cluster
2018/10/09 19:53:49 GradientNode clusterId: clfu7y1y6
2018/10/09 19:53:49 GradientNode nodeAttrs: {"cpuHostname":"ubuntu","cpuCount":2,"cpuModel":"Intel(R) Core(TM) i7-6700HQ CPU @ 2.60GHz","cpuFlags":"fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon nopl xtopology tsc_reliable nonstop_tsc eagerfpu pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ibrs ibpb stibp kaiser fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 invpcid rtm mpx rdseed adx smap clflushopt xsaveopt xsavec arat arch_capabilities","cpuMem":"8156872 kB","gradientNodeVersion":"6.7"}
```

## Node Attributes 

The `nodeAttrs` variable describes the CPU and GPU specs associated with the gradient-node. It also outputs all CPU flags which may be relevant for certain high performance machine learning libraries. You may specificy node attributes as arguments to the job - for example specify to run jobs only on a node with cpuCount = 4. If you do not have a node associated with your account that fulfills those parameters the job will stay in a pending state. 

## User Mounted Volumes
The `--mount` command is used for mapping one or multiple user mounted volumes to the docker container running the job. The syntax is as follows for each mount: 
```
/path/to/local:path/inside/job-container
```
Multiple volume mounts can be specified in one command by seperating via comma. Certain paths are restricted: do not mount /artifacts, /paperspace or / (root) volumes. Note the home directory inside the container is `/paperspace`. Example:
```
--mounts "/home/paperspace/gradient-node:/paperspace/hi,/home/paperspace/volume-test:/paperspace/bye"
```

