# Types of Storage

## Overview

Gradient° offering includes three types of storage that are available within the context of running a job or notebook container. Each kind has a different purpose. The three storage types are **Persistent, Artifact,** and **Workspace** storage.

## Persistent Storage

Persistent storage is a separate area where you can read and write files during a Job. You can also read and write data from your Workspace, but as the name indicates, persistent storage persists across job runs. Persistent storage is backed by a filesystem and is ideal for storing data like images, datasets, model checkpoints etc.  Learn more about persistent storage [here.](https://support.paperspace.com/hc/en-us/articles/360001468133-Persistent-Storage)

## Artifact Storage

Artifact storage is collected and made available after the job run in the CLI and web interface. You can find the Artifacts in the Paperspace console by going to the Gradient° Job Runner, clicking on the job run, and scrolling to the bottom of the output. From there you can download any files that your job has placed in the `/artifacts` directory.  If you need to get result data from a job run out of Paperspace, use the Artifacts directory.

The total of Workspace storage and Artifact storage cannot exceed the available storage on the host machine \(about 2 Terabytes\). If you think you will write enough files to fill this up, be sure to check for errors from the OS.

