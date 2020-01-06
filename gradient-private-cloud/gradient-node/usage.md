# Usage

## **Usage of gradient-node**

```text
$ gradient-node [--apiKey ] [--name ] [--id ] [--cluster ] [--clusterId ] [--logHost ]
```

`--apiKey string` Paperspace api key value.

`--cluster string` Cluster Name for this node. If no cluster with this name exists a new one will be created.

`--clusterId string` Cluster ID for this node, e.g. "cXXXXXXXX". Takes precedence over the Cluster Name option if both are specified.

`--debug` Debug mode \(verbose logging\).

`--id string` Node ID, e.g. "cmXXXXXXXXXXXXXX". If specified with the Node Name option, the node name will be updated.

`--name string` Node Name; defaults to the current hostname. Specify with the --id  option to changed the name of an existing node.

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
GRADIENT_NODE_DEBUG=[‘true’|’false’]
```

## **Root privileges**

Gradient-node needs to run with root privileges in order to communicate with docker on the host machine.  Therefore, if you are not running under a root account, you need to invoke gradient-node using sudo, e.g.:

```text
sudo ./gradient-node --apiKey XXXXXXXXXXXXXXXX    
```

## **Required Parameters**

The `--apiKey <key>` option is the only required parameter.  However it may also be provided via an environment variable, `GRADIENT_NODE_API_KEY=<key>`.

## Naming and Registration

On startup gradient-node will attempt to register in the account associated with the provided api key, using a default or provided node name, and return a unique id for the name. By default it will use the local hostname as the name of the instance. Each time gradient-node is run with a unique name a new cluster machine entry with a unique id is created unless a node id is also provided. The `--name` option can be used to override the default name.

If a gradient-node instance with the same name already exists within the cluster then all running nodes with the same name will be eligible to run jobs. The Gradient Web UI ****will only show one entry for each distinct node id however.

If you run gradient-node on a second machine, either make sure the second machine has a distinct hostname, or provide the `--cluster`  option with a distinct name. If you want the new instance to take over for an existing instance with the same name then you must stop any other currently running instances registered with that name. You can use the Gradient Web UI to check for active running instances with that name.

If you want to change the name of a gradient-node instance you can specify the `--id`  option, along with the new name using the `--name`  option. This will update the name associated with that gradient-node id.

## Specifying a Cluster

Each gradient-node instance is part of a unique private cluster within the user’s account. When starting gradient-node you can specify the cluster to register in using the `--cluster <name>`  or the `--clusterId <cluster_id>`  option. However if both are provided, the `--clusterId <cluster_id>`  option takes precedence.

If no cluster name or cluster id is specified when running gradient-node the instance is registered in the user account’s default cluster. The initial name for this cluster is “GradientNode Cluster”.

If you are a registering gradient-node for the first time in your account, you can pick a different name for the default cluster using the `--cluster <cluster_name>`  option. On subsequent runs you can omit the cluster name option if you want to register the gradient-node instance in the same default cluster. Note that certain cluster names are protected and should not be used: "PS Jobs", "PS Jobs on GCP", "PS Notebooks", "PS Notebooks on GCP" are not valid names for a gradient-node cluster. 

After the first cluster is created, if you register a node specifying a different cluster name, then a new cluster with that new name will automatically be created. However, it will not be the default cluster for the account.

In the Gradient Web UI you can change the cluster name for any cluster in your account and/or switch which cluster is currently the default. When scheduling jobs you can select the targeted cluster using the Paperspace CLI or SDK job create options. You may target a specific node within a cluster by specifying the name or the node attributes of the node. 

## Jobs Scheduling

Here are the job create options which are used to run a job to run on a specific gradient-node instance:

* `--machineType "GradientNode"`  \(Restricts the job to running on a gradient-node instance. If no other scheduling option is given the job will be scheduled in the default cluster for the account.\)
* `--cluster <cluster_name>` or `--clusterId <cluster_id>`  \(Restricts the job to running on a cluster in the user’s account with the given name or id. If this option is specified, machineType “GradientNode” is assumed.\)
* `--nodeAttrs <json_object>`  \(Restricts the job to running on a gradient-node instance which has the specified node attribute values, expressed in the form of a JSON object definition. See [Node Attributes](job-scheduling-and-node-attributes.md).\)

## Example Output on Startup

The following shows a sample of log messages generated when starting and registering gradient-node. The `name`, `id`, `cluster`, and `cluserId`parameters are displayed, along with the node attributes structure, `nodeAttrs`, which is described below.

```text
2018/10/09 19:53:48 Starting gradient-node 6.7 ba95b2d 2018-10-09_18:12:45_UTC
2018/10/09 19:53:49 GradientNode name: ubuntu
2018/10/09 19:53:49 GradientNode id: cmdc2sjlenkhwx
2018/10/09 19:53:49 GradientNode cluster: GradientNode Cluster
2018/10/09 19:53:49 GradientNode clusterId: clfu7y1y6
2018/10/09 19:53:49 GradientNode nodeAttrs: {"cpuHostname":"ubuntu","cpuCount":2,"cpuModel":"Intel(R) Core(TM) i7-6700HQ CPU @ 2.60GHz","cpuFlags":"fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon nopl xtopology tsc_reliable nonstop_tsc eagerfpu pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ibrs ibpb stibp kaiser fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 invpcid rtm mpx rdseed adx smap clflushopt xsaveopt xsavec arat arch_capabilities","cpuMem":"8156872 kB","gradientNodeVersion":"6.7"}
```

## Run a job via gradient-node

```text
paperspace jobs create --container Test-Container --cluster "GradientNode Cluster" --command 'ls -l' --workspace none
```



