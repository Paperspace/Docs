---
description: This guide explains how instances and kernels are used in Gradient Notebooks
---

# Machines

## Introduction to notebook machines

Gradient makes a wide variety of machines available for use with notebooks. A full list of instance types provided by Gradient is available here:

{% content-ref url="../../more/instance-types/" %}
[instance-types](../../more/instance-types/)
{% endcontent-ref %}

The first opportunity to select a machine is in the `Select a machine` section when creating a new notebook.

![Gradient makes machines available in the Select a machine section when creating a notebook.](<../../.gitbook/assets/create a notebook instance type.gif>)

Gradient Notebooks makes it easy to swap out a machine for a different machine at any time -- so keep that in mind when deciding what machine to select. It's common to start with a less powerful machine and upgrade as needed over time.

## How to select a machine when creating a notebook

When creating a new notebook, the `Select a machine` section of the notebook create workflow provides a list of GPU-backed and CPU-backed machines available for use.

![When creating a new notebook, we can select from a long list of GPU and CPU-backed machines.](<../../.gitbook/assets/gpu and cpu machines.gif>)

If a machine is available for use it will be listed under the `Available` heading. If a machine is out of capacity it means that all instances are currently being used by other Paperspace users.&#x20;

## How to swap machines in an existing notebook

To swap instances in an existing notebook, use the **Instance** selector available on the left side of the notebook.&#x20;

If the notebook is currently in the **Running** state, it will first need to be stopped.

![Use the Instance tab on the left side of the notebook to manage compute instances.](<../../.gitbook/assets/stop instance.gif>)

After the instance is stopped, a new instance can be selected from the list of available machines.

![Select a new instance using the instance selector available on the left side of the notebook.](<../../.gitbook/assets/instances available in notebook.gif>)

The top bar will indicate when a notebook is again in the **Running** state.

## How to use a machine that is unavailable

If an instance type is at capacity it will be listed as `Unavailable`. Popular instance types, such as instances providing free gpus, sometimes reach capacity during busy periods.&#x20;

![When machines are at capacity, they are marked as Currently Unavailable. It's recommended to wait a few minutes and check back to see if capacity has opened up or else to try a different machine type that is available.](<../../.gitbook/assets/unavailable instances.png>)

If the machine type that we require is listed as unavailable, we'll need to wait until capacity frees up. We should first try waiting a few minutes and refreshing the page. If capacity is still not available, we might try a different instance with better availability or come back during a less busy time of day.

{% hint style="info" %}
Free GPU instances in particular are often in high demand. Try using popular free resources outside of peak hours (MF 9:00AM - 5:00PM ET) or try using more powerful paid machines.
{% endhint %}

Paperspace is constantly adding capacity to its datacenters. The [Changelog](https://updates.paperspace.com) is a good resource to hear about capacity upgrades. If you are repeatedly running into capacity issues with a particular machine type, please [let us know](https://support.paperspace.com/hc/en-us/requests/new).&#x20;

## How to use the auto-shutdown timer

The auto-shutdown timer is a useful feature that automatically shuts down a notebook after a pre-determined amount of time. The timer starts from the moment that the notebook is started.

![Setting the auto-shutdown timer to 4 hours.](<../../.gitbook/assets/autoshutdown timer.gif>)

When a notebook is running, the amount of time remaining until auto-shutdown is displayed in the **Instance** tab.

![The duration remaining on the auto-shutdown timer is visible in the Instance pane.](../../.gitbook/assets/auto-shutdown-example.png)

It is currently not possible to alter the auto-shutdown interval after it has been set.

## How to view kernel state

Gradient allows the user to start an arbitrary number of kernels within the notebooks IDE. A kernel is [a programming language specific process](https://docs.jupyter.org/en/latest/projects/kernels.html) that runs independently of other kernels on a virtualized machine. Gradient uses the [IPython](https://ipython.readthedocs.io/en/stable/index.html#ipython-documentation) Jupyter kernel.&#x20;

In Gradient Notebooks, the kernel state is visible in the file manager as well as in the top bar.

![Kernel state is visible in the file manager as well as in the top bar.](../../.gitbook/assets/kernels.png)

The kernel state is made accessible in the top bar as text. In the image above, for example, the top bar is indicating that the kernel state is **Running**.

## How to restart a kernel

One of the benefits of kernels is the ability to restart a single kernel without disrupting the rest of the notebook. This is useful when a notebook is stuck or unresponsive.&#x20;

An individual kernel may be restarted using the `Restart Kernel` button in the top right of the notebooks IDE.&#x20;

![Use the Restart Kernel button in the top right to restart a stuck process.](<../../.gitbook/assets/restart kernel.gif>)

It's also possible to stop or restart the kernel using the 3-dot menu next to an individual file in the file manager.

![It's also possible to use the 3-dot menu to stop or restart a kernel.](../../.gitbook/assets/restart-stop-kernel-file-manager.png)

If restarting the kernel does not fix an issue with a stuck process, it may be necessary to stop and restart the entire notebook. In this case we would select `Stop Instance` and wait for the instance to shutdown before selecting a new instance to start.
