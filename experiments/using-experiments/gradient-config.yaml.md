# Gradient Config File

## Using config.yaml to run experiments

Gradient supports using a config.yaml to execute experiments using the CLI. If you find yourself repeatedly typing the same commands or doing various kinds of automation or pipelining and want the configuration to be reusable and checked into source control, this tool is for you. 

### Generating a config.yaml template

You can create a config.yaml template with all of the possible parameters defined by using the `--createOptionsFile` flag.

```bash
$ gradient experiments run singlenode --createOptionsFile config_file_name.yaml
```

### Running experiments using a config.yaml

Once you have filled out the needed parameters, execute an experiment with the `--optionsFile` flag set.

```
 gradient experiments run singlenode --optionsFile config.yaml
```

### Sample config.yaml

A sample config.yaml file for single node experiments is displayed below

{% hint style="info" %}
There are many other parameters that you may want to use when running an experiment.
{% endhint %}

{% code title="config.yaml" %}
```bash
apiKey: null
command: python mnist.py
container: tensorflow/tensorflow:1.13.1-gpu-py3
experimentEnv:
  EPOCHS_EVAL: 5
  EVAL_SECS: 10
  MAX_STEPS: 1000
  TRAIN_EPOCHS: 10
machineType: P4000
modelPath: /artifacts
modelType: Tensorflow
name: experiment name
projectId: <project id> 
registryPassword: null
registryUrl: null
registryUsername: null
tensorboard: false
tensorboard_set: null
workspace: 'https://github.com/Paperspace/mnist-sample.git'
workspaceRef: null
datasetUri:
  - "s3://some.dataset/uri"
  - "s3://some.other.dataset/uri"
datasetName:
  - "some dataset name"
  - null
datasetAwsAccessKeyId:
  - none
  - some_other_key_id
datasetAwsSecretAccessKey:
  -
  - some_other_secret
datasetVersionId:
datasetEtag:
  - "some etag"
  - "some other etag"
```
{% endcode %}

