# Environment Variables

Information can be passed to and from Workflows, and between the jobs within them.

One form of this is our [Workflow input/output](https://docs.paperspace.com/gradient/explore-train-deploy/workflows/understanding-inputs-and-outputs), which can be datasets, volumes or strings.

Another is environment variables. These are used when we want to pass information in the Workflow YAML to some other computation being called, such as authenticating to a private GitHub repository, or running a Python `.py` script.

### Why use environment variables and not just arguments to a script?

Some reasons are

* Environment variables can hold other information like [secrets](https://docs.paperspace.com/gradient/get-started/managing-projects/using-secrets), that are harder to pass securely otherwise.
* They can be defined as applying to all Workflow jobs (under `defaults:`), or per-job, under a job's name.
* Sets of arguments may be used several times, for example, the potentially large number of hyperparameters for training an ML model may want to be made explicit in a script. Then we may want to use them for training more than one model, varying some parameters but leaving the rest unchanged.
* Using environment variables makes larger setups like this easier to handle than passing large argument lists more than once, helping ensure different model invocations get the same settings when they should be getting them.

### Specifying environment variables in Workflows

An environment variable global to a script comes under `env:` in the `defaults:` field. An example that is commonly used is the secret to hold the user's API key, and the code block containing it, defining the environment variable `HELLO` might look like

```yaml
defaults:
  env:
    HELLO: secret:hello
  resources:
    instance-type: P4000
```

Common job-specific environment variables are information to be passed to a script, for example, the model hyperparameters from our [Deep Learning Recommender tutorial](https://docs.paperspace.com/gradient/get-started/tutorials-list/end-to-end-example) appear in this code:

```yaml
RecommenderTrain:
  needs:
    - CloneRecRepo
  inputs:
    repoRec: CloneRecRepo.outputs.repoRec
  env:
    HP_FINAL_EPOCHS: '50'
    HP_FINAL_LR: '0.1'
  outputs:
    trainedRecommender:
      type: dataset
      with:
        ref: recommender
  uses: script@v1
  with:
    script: |-
      cp -R /inputs/repoRec /Deep-Learning-Recommender-TF
      cd /Deep-Learning-Recommender-TF
      python workflow_train_model.py
    image: tensorflow/tensorflow:2.4.1-jupyter
```

Here, the number of epochs to train the final model, `HP_FINAL_EPOCHS: '50'`, and the model's learning rate, `HP_FINAL_LR: '0.1'`, are used by the `workflow_train_model.py` Python script that the job calls.

### Using values of Workflow environment variables in scripts

To utilize the values of the Workflow environment variables in a script, the user parses them as part of their code. In the recommender case here we pass them to variables in the code:

```python
hp_final_epochs = int(os.environ.get('HP_FINAL_EPOCHS'))
hp_final_lr = float(os.environ.get('HP_FINAL_LR'))
```

Python's `os.environ` reads the values, and we need to cast them to the correct data type integer, float, etc.) for the model to understand them.

#### Advanced Usage

For more advanced situations, Python has libraries such as [env\_config](https://pypi.org/project/env\_config). This overlaps somewhat with what Workflows can do, because it allows you to declare environment variables as well. But it has clearer handling of issues like data types and errors, and can handle variables that are lists (useful for hyperparameter tuning), or more complex structures.

It can read declared variables from a file, e.g., `test.sh`, from `env_config`'s [GitHub page](https://github.com/flowpl/env\_config):

```bash
#!/usr/bin/env bash

# comment is ignored

HIDDEN_VARIABLE="value not parsed"
export VISIBLE_VARIABLE_1="this value will be available"

function {
   # if the line does not start with export it's ignored
}

# variables inside strings are not expanded. The value will contain the literal :code:`$OTHER_VARIABLE`.
export VARIABLE_CONTAINING_REFERENCE="$OTHER_VARIABLE"

read in by

from env_config import Config, parse_str

# uses the value of CONFIG_FILE as the file name to load variables from
config = Config(filename_variable='CONFIG_FILE', defer_raise=False)
# visible_variable_1 is declared in test and the current tag is test. variable1 will be loaded from test.sh
config.declare('visible_variable_1', parse_int(), ('test',), 'test'))

# visible_variable_2 is declared in the 'default' tag and not available in the config file.
# visible_variable_2 will be ignored because the current tag is 'test'
config.declare('visible_variable_1', parse_int(), ('default',), 'test')
```

This could potentially be integrated with Workflows to similarly handle a set of Workflow environment variables.
