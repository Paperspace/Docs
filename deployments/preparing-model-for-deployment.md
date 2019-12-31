---
description: Train and output a Tensorflow Model
---

# Prepare Models for Deployment

This example code demonstrates how to use TensorFlow to export a trained model so that it is compatible Tensorflow Serving and Gradient Model Deployments.  The code below should be incorporated into your experiment, and assumes you are using Tensorflow 1.x with Python.

Note: you must specify `--modelPath /artifacts` when running the experiment, in order to have the model parsed and uploaded by Gradient. Learn more about [model path options](../models/model-path.md) here.

### Example 

```text
# Set export dir
export_dir = os.path.abspath(os.environ.get('PS_MODEL_PATH', os.getcwd() + '/models'))

# Define Model
mnist_classifier = tf.estimator.Estimator(
        model_fn=model_function,
        model_dir=flags_obj.model_dir,
        config=run_config,
        params={
            'data_format': data_format,
        })
image = tf.placeholder(tf.float32, [None, 28, 28])

# Define Input
input_fn = tf.estimator.export.build_raw_serving_input_receiver_fn({
            'image': image,
            })
# Export Model using builtin tensorflow export_savedmodel
mnist_classifier.export_savedmodel(flags_obj.export_dir, input_fn,
                                   strip_default_attrs=True)
tf.logging.debug('Model Exported')


```

The code above first gets the specified `--modelPath` from parameters used to run the experiment using the environment variable `PS_MODEL_PATH`, which is available to the experiment while it is running. \(Note: if `--modelPath` was not specified, the model export directory defaults to `./models` using the code above.\)

It then uses TensorFlow's [SavedModelBuilder module](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/saved_model/builder.py) to export the model. `SavedModelBuilder` saves a "snapshot" of the trained model to 

```text
os.path.abspath(os.environ.get('PS_MODEL_PATH', os.getcwd() + '/models'))
```

  so that it can be loaded later for deployments.

### SavedModel format

For details on the SavedModel format, please see the documentation at [SavedModel README.md](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/saved_model/README.md).



