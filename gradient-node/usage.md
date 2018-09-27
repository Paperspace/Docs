# Usage

## **Usage of gradient-node**

gradient-node \[--apiKey \] \[--name \] \[--id \] \[--cluster \] \[--clusterId \] \[--logHost \]

--apiHost string Gradient API Host \(default "[https://gradient-api.paperspace.io](https://gradient-api.paperspace.io)"\).

--apiKey string Paperspace api key value.

--cluster string Cluster Name for this node. If no cluster with this name exists a new one will be created.

--clusterId string Cluster ID for this node, e.g. "cXXXXXXXX". Takes precedence over the Cluster Name option if both are specified.

--debug Debug mode.

--id string Node ID, e.g. "cmXXXXXXXXXXXXXX". If specified with the Node Name option, the node name will be updated.

--logHost string Gradient Log Host \(default "[https://logs.paperspace.io](https://logs.paperspace.io)"\).

--name string Node Name; defaults to the current hostname. Specify with the --id  option to changed the name of an existing node.

Optional ENVIRONMENT VARIABLES: \(These can be used to configure the options above via environment settings. Note that any command line options take precedence over the environment settings.\)

```text
GRADIENT_NODE_API_KEY= GRADIENT_NODE_NAME= GRADIENT_NODE_ID= 
GRADIENT_NODE_CLUSTER= GRADIENT_NODE_CLUSTERID= GRADIENT_NODE_API_HOST= 
GRADIENT_NODE_LOG_HOST= GRADIENT_NODE_DEBUG=[‘true’|’false’]
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

If a gradient-node instance with the same name already exists within the cluster then all running nodes with the same name will be eligible to run jobs. The Gradient web UI ****will only show one entry for each distinct node id however.

If you run gradient-node on a second machine, either make sure the second machine has a distinct hostname, or provide the `--cluster`  option with a distinct name. If you want the new instance to take over for an existing instance with the same name then you must stop any other currently running instances registered with that name. You can use the Gradient web UI to check for active running instances with that name.

If you want to change the name of a gradient-node instance you can specify the `--id`  option, along with the new name using the `--name`  option. This will update the name associated with that gradient-node id.

## Specifying a Cluster

Each gradient-node instance is part of a unique private cluster within the user’s account. When starting gradient-node you can specify the cluster to register in using the --cluster  or the `--clusterId`  option. However if both are provided, the `--clusterId`  option takes precedence.

If no cluster name or cluster id is specified when running gradient-node the instance is registered in the user account’s default cluster. The initial name for this cluster is “GradientNode Cluster”.

If you are a registering gradient-node for the first time in your account, you can pick a different name for the default cluster using the `--cluster`  option. On subsequent runs you can omit the cluster name option if you want to register the gradient-node instance in the same default cluster.

After the first cluster is created, if you register a node specifying a different cluster name, then a new cluster with that new name will automatically be created. However, it will not be the default cluster for the account.

In the Gradient web UI you can change the cluster name for any cluster in your account and/or switch which cluster is currently the default. When scheduling jobs you can select the targeted cluster using the paperspace CLI or API job create options.

