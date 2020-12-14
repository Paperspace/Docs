# Gradient SDK Overview

## About

{% hint style="info" %}
Read the [announcement](https://blog.paperspace.com/new-gradient-sdk/) on our blog which includes a [sample project](https://ml-showcase.paperspace.com/projects/gradient-python-sdk-end-to-end-example) you can run!
{% endhint %}

The SDK let's you programmatically interact with the Gradient platform.  The SDK is designed for maximum flexibility and is useful in many different scenarios.  Some examples include interactively launching experiments and deployments \(model serving\), streaming your experiment logs into a Jupyter environment, or incorporating the SDK into your python project to build sophisticated pipelines.  

The SDK is fully compatible with our CLI which uses this SDK under the hood.  

The SDK was built to be "pythonic" in the sense that everything is a python object.  For example, you can add input parameters to any of the commands as a dictionary which you can then call as a function to unpack the dictionary.  All create commands eg _create experiment_, return the experiment's ID.  These IDs can then be easily be chained together to create a pipeline.  For example, you can query a model for it's accuracy and compare that model to other trained models. 

Get help anytime by calling the `help` function on any object.  

## Install

The SDK is bundled with the Gradient CLI.  You'll need the latest version which you can download by adding `--pre` when [installing \(or upgrading\) the CLI](../../get-started/install-the-cli.md).  

## Examples

There are examples for each section of the SDK starting [here](projects-client.md).  We also offer a full end-to-end tutorial [here](../sdk-tutorial.md).

