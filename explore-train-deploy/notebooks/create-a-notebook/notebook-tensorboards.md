---
description: This guide explains how to use TensorBoard within Gradient Notebooks
---

# TensorBoard

## Introduction to TensorBoard

TensorBoard is a [visualization toolkit](https://www.tensorflow.org/tensorboard/) from TensorFlow. It is useful for a variety of applications including visualizing metrics and histograms, displaying images, and more.&#x20;

![Example TensorBoard](https://s3-ap-southeast-1.amazonaws.com/blob.blankcursor.com/uploads/editor\_attachment/attachment/5650/792a03f09ffcf0db65f4f6fccfe20e561571de8d\_2\_1117x586.png)

To get started with TensorBoard, we'll need to run a command in the terminal and then access a special URL.

## How to configure a TensorBoard in Gradient Notebooks

To run TensorBoard in a notebook, first make sure that the notebook has TensorBoard installed.&#x20;

Next, open a notebook [terminal](../notebook-terminals.md) and run the following command:

```
tensorboard --logdir . --bind_all
```

If needed, the `--logdir` path may be changed to a different value.&#x20;

The TensorBoard is now available at the following URL:

```
https://tensorboard-NOTEBOOKID.CLUSTERID.paperspacegradient.com
```

`NOTEBOOKID` may be found on the notebook list view in the Gradient console.&#x20;

The default `CLUSTERID` value is `clg07azjl`. Private clusters will have a `CLUSTERID` on the clusters page.
