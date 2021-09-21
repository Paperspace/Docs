# SDK

## About

The SDK lets you programmatically interact with the Gradient platform. The SDK is designed for maximum flexibility and is useful in many different scenarios. Some examples include interactively launching [Workflows](../../explore-train-deploy/workflows/) and [Deployments]() \(model serving\), or incorporating the SDK into your python project to build a custom workflow.  

The SDK was built to be "pythonic" in the sense that everything is a python object. For example, you can add input parameters to any of the commands as a dictionary which you can then call as a function to unpack the dictionary. All create commands, e.g., _create workflow_, return the object's ID. These IDs can then be easily be chained together to create a pipeline. For example, you can query a model for its accuracy and compare that model to other trained models. 

Get help anytime by calling the `help` function on any object.  

## Install

The SDK is bundled with the [Gradient CLI](../../get-started/quick-start/install-the-cli.md).  

## Examples

There's an overview page covering each section of the SDK starting [here](projects-client.md).  We also offer some example commands [here](sdk-tutorial.md).

