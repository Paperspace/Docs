---
description: >-
  This document covers common Gradient errors and what they mean. Should you
  submit a support ticket, please provide the error message and any pre-emptive
  behavior.
---

# Common Errors

### User Errors

#### Error downloading artifacts

We were unable to download the workspace from the URL you provided. Check your notebook logs for details.

#### Exceeded timeout of 120 seconds. Waiting for readiness.

The jupyter kernel for your notebook did not start in a reasonable amount of time. Be sure to check your notebook logs for any start up issues.

#### Failed to pull image: Image does not exist

The supplied container image does not exist on the supplied container registry.

#### Exceeded timeout of 1800 seconds waiting for image pull

We limit image pulls to 1800 seconds. We recommend trimming down the size of your container to ensure it can start quickly for the best user experience. Containers should only contain installed packages and configuration - data should be kept in `/notebook` or `/storage`

#### Command \[...] exited with code 1

Your jupyter kernel crashed with a failure exit code. Check your notebook log for error messages.

#### Command \[...] exited with code 127

This error occurs most with custom containers. It means that the executable was not found in your path. You may have made a typo in your command, or you can fully elaborate the path e.g. `/home/jovyan/jupyter` instead of just `jupyter`

#### Command \[...] exited with code 137

Your notebook has used too much memory and has been terminated to preserve the experience of other customers. You can try using a larger machine type or profiling your notebook to ensure you are within the limits of the system.

### Internal Errors

#### Error uploading notebook workspace

We encountered an internal error uploading `/notebook` for offline viewing and forking. Your next notebook start should retain all of its files, but the offline viewer and new forks may not pick up your latest changes.

#### Failed to pull image

We were unable to pull your container. Temporary network errors are often the cause of this failure, particularly for large containers. Trying to start your notebook again should have better luck.

#### Error caching notebook image

We were unable to take a snapshot of your notebook environment. Files that are not in `/storage` or `/notebooks `created during this run of the notebook may not have uploaded. These files are usually newly installed `apt` or `pip` packages. Your next run will use the last successful snapshot.

#### Notebook was terminated Early

Your notebook was preempted before teardown could begin. Usually, this error message appears because the machine your notebook was on has crashed.

#### Error creating container

We were unable to start the container on the host system.

#### Failed to send the notebook to the cluster

There was an issue forwarding the notebook to the cluster, and it has not been able to start. You have not been billed, and we recommend retrying the notebook start. Check our [status page](https://status.paperspace.com) for any ongoing issues.

#### Internal error

We were unable to process your notebook for unspecified reasons. Check our [status page](https://status.paperspace.com) for any ongoing issues.

