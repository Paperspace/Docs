# Environment Variables

You can configure your code to accept external parameters at runtime, overriding default any values in your code.  These parameters, called _Experiment Environment Variables_, are automatically captured and tracked in Gradient.  

#### Code sample:

```python
train_epochs=int(os.environ.get('TRAIN_EPOCHS', 40)),
epochs_between_evals=int(os.environ.get('EPOCHS_EVAL', 100)),
batch_size=int(os.environ.get('BATCH_SIZE', 100)),
```

#### Adding parameters to Experiment:

The syntax for these parameters in the CLI is JSON.

```python
gradient experiments ... --experimentEnv "{\"EPOCHS_EVAL\":5,\"TRAIN_EPOCHS\":2,\"MAX_STEPS\":5,\"EVAL_SECS\":10}"  
```

These parameters will be injected into the Experiment at runtime and captured in Gradient.

![](../../.gitbook/assets/image%20%2811%29.png)

