---
description: Visualize and compare experiments with TensorBoards
---

# Overview

{% hint style="info" %}
Gradient TensorBoards are a Gradient Enterprise feature. [Contact Sales](https://info.paperspace.com/contact-sales) for inquiries!
{% endhint %}

**TensorBoard** is a popular open source visualization software that comes with any standard TensorFlow installation but is a first class citizen in other frameworks such as PyTorch. 

![](../.gitbook/assets/image%20%2854%29.png)

Here's a description of the TensorBoard project by Google:

> “The computations you’ll use TensorFlow for many things \(like training a massive deep neural network\) and they can be complex and confusing. To make it easier to understand, debug, and optimize TensorFlow programs, we’ve included a suite of visualization tools called TensorBoard.”

TensorBoard was created as a way to help us understand the flow of tensors in your model so that you can debug and optimize it. It is generally used for two main purposes:

1. **Visualizing the Graph**
2. **Writing Summaries to Visualize Learning**

### Different Views of TensorBoard <a id="different-views-of-tensorboard"></a>

Different views take inputs of different formats and display them differently. You can change them on the orange bar at the top of a TensorBoard.

* **Scalars** - Visualize scalar values, such as classification accuracy.
* **Graph** - Visualize the computational graph of your model, such as the neural network model.
* **Distributions** - Visualize how data changes over time, such as the weights of a neural network.
* **Histograms** - A fancier view of the distribution that shows distributions in a 3-dimensional perspective
* **Projector** - Can be used to visualize word embeddings \(that is, word embeddings are numerical representations of words that capture their semantic relationships\)
* **Image** - Visualizing image data
* **Audio** - Visualizing audio data
* **Text** - Visualizing text \(string\) data

{% hint style="info" %}
[See the official docs](https://www.tensorflow.org/tensorboard) for more info!
{% endhint %}

### TensorBoards on Gradient

On Gradient, each TensorBoard runs on a dedicated, lowest-horsepower CPU-only machine instance from within your cluster; as such, they are not just database resources. This means that creating TensorBoards, adding experiments to them, and removing experiments from them, can sometimes take a couple of minutes.

When you Add an experiment to a TensorBoard, the experiment status will remain in an Adding state until the experiment has completed.

TensorBoards can be protected via basic authentication, the Username and Password for which can be set upon creation.

Next you'll learn how to use TensorBoards on Gradient using the UI, the CLI, and [via scripting in TensorFlow](using-tensorboards/getting-started-with-tensorboards.md).

