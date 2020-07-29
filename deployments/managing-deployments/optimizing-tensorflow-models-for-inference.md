# Optimize Models for Inference

Gradient supports deployment of models compatible with industry standards such as TensorFlow. There are a variety of optimizations you can perform on TensorFlow neural network graphs to reduce their size and latency for inference. Because we use [TF Serving](https://github.com/tensorflow/serving) for TensorFlow models, we are able to support deployment of these optimized graphs.

Gradient also supports any models pruned, quantized, etc. using third-party tools.  You can leverage these tools outside of Gradient \(eg import an optimized model\) or as an automated step in your machine learning pipeline.  [OpenVINO](https://docs.openvinotoolkit.org/) is an example of a popular optimization framework that is supported on Gradient.





