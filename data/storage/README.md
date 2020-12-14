# Types of Storage

## Overview

Gradient includes three types of storage that are available within the context of running an Experiment, Job or Notebook. The three storage types are **Persistent, Artifact,** and **Workspace** storage.  Additionally, there is an option to mount S3 compatible object storage datasets to a running experiment which are called **Private Datasets**.  

## Persistent Storage

Persistent storage is a high-performance storage directory located at `/storage` where you can read and write files. Persistent storage is backed by a filesystem and is ideal for storing data like images, datasets, model checkpoints etc.  Anything you store in the `/storage` directory will be accessible across multiple runs of Experiments, Jobs and Notebooks in a given storage region. 

Persistent Storage is kept in three regions based on your machine type or tier:

1. PS East Coast \(NY2\)
2. GCP West
3. PS West Coast \(for the [Free Tier](../../instances/free-instances.md) on Gradient\)

{% hint style="warning" %}
Persistent Storage is specific to each region. This means that data in your Persistent Storage for the Free Tier is not be accessible from paid instance types, and vice versa.
{% endhint %}

## Artifact Storage

Artifact storage is collected and made available after the Experiment, Job, or Notebook run in the CLI and web interface. You can find the Artifacts in the Gradient console, clicking on the job run, and scrolling to the bottom of the output. From there you can download any files that your job has placed in the `/artifacts` directory.  If you need to get result data from an Experiment, Job, or Notebook run out of Gradient, use the Artifacts directory.

The total of Artifact storage cannot exceed the available storage on the host machine \(about 200 GB\). If you think you will write enough files to fill this up, be sure to check for errors from the OS.

## Workspace Storage

Workspace storage is temp storage available on the worker node while the Experiment, Job, or Notebook is running.  Workspace storage is imported from the location where your Experiment or Job was initiated \(either a local directory on your laptop or a remote git repo\).  The contents of that directory are zipped up and uploaded to the container in which your Experiment or Job runs. 

The Workspace exists for the duration of the job run. This directory is located at `/home/paperspace` if you need to reference the absolute path. If you need to push code up to Paperspace and run it, using the Workspace storage is the way to do it.

The total of Workspace storage cannot exceed the available storage on the host machine \(about 200 GB\). If you think you will write enough files to fill this up, be sure to check for errors from the OS. 

## Private Datasets

Gradient provides the ability to mount S3 compatible object storage buckets to an experiment at runtime.  Learn more [here](../private-datasets-repository/).

