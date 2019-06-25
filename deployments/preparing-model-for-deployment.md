---
description: >-
  This tutorial shows you how to use TensorFlow Serving components to export a
  trained TensorFlow model and use the Gradient model deployments to serve it.
  Train and export TensorFlow model
---

# Preparing Model for Deployment

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

We use TensorFlow's [SavedModelBuilder module](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/saved_model/builder.py) to export the model. `SavedModelBuilder` saves a "snapshot" of the trained model to 

```text
os.path.abspath(os.environ.get('PS_MODEL_PATH', os.getcwd() + '/models'))
```

  so that it can be loaded later for deployments.

### SavedModel format

For details on the SavedModel format, please see the documentation at [SavedModel README.md](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/saved_model/README.md).



