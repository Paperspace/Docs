# Hyperparameter Tuning

## About

{% hint style="warning" %}
This feature is in beta. The documentation is not yet complete.
{% endhint %}

Gradient provides users the ability to tune hyperparameters for their machine learning models, harnessing the power of our cloud to explore different model configurations and discover an optimal model.

## Initiating

### For a GradientCI \(GitHub-integrated\) project

See [GradientCI documentation](../projects/gradientci.md) for information on how experiments can be triggered from code pushed to your GitHub repository.

In the Python script file you configure as your `command`, specify the domain of parameters over which Hyperopt should search.

{% code-tabs %}
{% code-tabs-item title="main.py" %}
```python
from paperspace-sdk import hyper_tune
from .model import train_model
hparam_def = {
        'dense_len': 8 + hp.randint('dense_len', 120),
        'dropout': hp.uniform('dropout', 0., 0.8),
        'activation': hp.choice('activation', ['relu', 'tanh', 'sigmoid'])
}

hyper_tune(train_model, hparam_def,algo=tpe.suggest, max_evals=25)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* `dense_len` is how many layers the DNN has
* `dropout` here is a uniform distribution between 0% and 80% dropout
* `activation` here tests different common activation functions
* The `hyper_tune` function executes the hyperparameter tuning experiment
* The `algo` parameter accepts `tpe.suggest` where the Hyperopt library chooses a default algorithm, but you can also choose others
* The `max_evals` parameter determines how many search trials to run total

### For a standalone projects

In your [experiment call to the Paperspace CLI](run-experiments.md), enter this script file name as `--command`.

## Viewing hyperparameter search progress

To see the progress of your hyperparameter search experiment, navigate to your GradientCI project in the Gradient application. Select the hyperparameter search experiment and go to the "Hyperparameters" tab. You will see a visual display of all the jobs triggered by the experiment.

## Selecting the optimum model

Once the hyperparameter search is finished, Gradient automatically saves the highest-performing model as the model output of you experiment.

