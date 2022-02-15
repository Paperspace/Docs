# Core Concepts

As a data science platform that encompasses both notebook-based and IDE-based functionality, with exploratory and production work in scope, Gradient contains a number of core concepts that help everything function.

Some of these give meanings to words (e.g., Notebook) that are more specific than their general meaning, and in these cases we capitalize them to indicate that we are referring to the Gradient embodiment of the concept.

{% hint style="info" %}
This page focuses on concepts specific to Gradient. For a more general overview of concepts related to AI and machine learning, take a look at our [AI Wiki](https://docs.paperspace.com/machine-learning/). It contains short & friendly explanations that aim to be accessible to all of our users.
{% endhint %}

{% embed url="https://youtu.be/Kg7CvboqBuU" %}

## Projects

A Gradient [Project](managing-projects/) is a collection of Notebooks, Workflows, Deployments, Models, and Data. It provides a way to organize your Gradient workloads into related groups and sharing within a team.

The layout of the tabs within a Project in the GUI reflects this:

![](../.gitbook/assets/project\_tabs.png)

Projects can be created standalone, or linked to a GitHub repository.

## Notebooks

A Gradient [Notebook](https://docs.paperspace.com/gradient/explore-train-deploy/notebooks) is a collection of files that are launched together on a Gradient instance that includes files in the `.ipynb` Jupyter notebook format. These can be edited and run through the Gradient Notebook interface, or the JupyterLab interface.

Launching a Notebook includes all the frameworks, libraries, and drivers you need for machine learning. Gradient Notebooks make it easy to explore data and coding concepts, experiment with machine learning models, and collaborate with other people on projects.

* No configuration required
* Free access to CPU and GPU instances
* Easy sharing

{% hint style="success" %}
Check out the [FREE GPU](../more/instance-types/free-instances.md) option when launching Notebooks!
{% endhint %}

## Workflows

Workflows provide automation for machine learning tasks such as orchestrating full end-to-end machine learning application development. Workflows let you use a [GitHub-action](https://docs.github.com/en/actions) style syntax to easily create powerful automation.

The format of a Workflow file is [YAML](https://en.wikipedia.org/wiki/YAML), a fragment of which looks like this:

```yaml
uses: script@v1
with:
  script: |-
    echo 'hello world'
    echo $RANDOM
  image: bash:5
```

Workflows can call other scripts, such as a Python `.py` containing arbitrary Python code, and can be triggered to run from a GitHub repository linked to a project when placed in the repository's `./gradient/workflows` directory.

## Deployments (inference/model serving)

Once a model is created, you can easily serve the model high-performance, low-latency micro-service with a RESTful API. Learn more [here](https://docs.paperspace.com/gradient/explore-train-deploy/deployments-preview).

## Models

A [machine learning model](https://docs.paperspace.com/machine-learning/wiki/machine-learning-models-explained) is a file or collection of files that describe an arbitrary transformation to be made on an input dataset to produce an output. Often, the transformation is in the form of a mapping from a set of input features to an output such as a prediction, recommendation, text, or image.

You can either upload a model or generate models from your training workloads which can be stored in the [Gradient Model Repository](../data/models/). Models in the repository are versioned.

We support common model formats including TensorFlow, ONNX, or custom.

## Data

In Gradient, a Dataset refers to a versioned collection of files, which in turn might be individual datasets. These of course can be much larger than the other common method of curating a set of versioned files, a GitHub repository.

#### [**Versioned Data**](../data/data-overview/private-datasets-repository/)

Versioned Datasets are used to manage the flow of data with your machine learning workloads. Datasets have immutable versions that can be used to track your data as it changes. Datasets can be used as input to Gradient workloads as well as outputs. Gradient provides the ability to mount S3 compatible object storage buckets at runtime. Learn more [here](../data/data-overview/private-datasets-repository/).

#### [Persistent Storage](../data/data-overview/#persistent-storage)

Persistent storage is a persistent filesystem automatically mounted on every Notebook and is ideal for storing data like images, datasets, model checkpoints, and more. Gradient Dataset versions are automatically cached to persistent storage for performance. Learn more [here](../data/data-overview/#persistent-storage).

## Other concepts

While the above are the main core concepts, users will encounter others while navigating Gradient. Some of them are:

* **API key / secret:** Users need an API key to authenticate to Gradient when performing certain actions, for example, from the command line on one's own machine. Other non-public information such as GitHub credentials can also be stored, as secrets.
* **Cluster:** Many users or teams will have access to their own Gradient or other hardware on which workloads can be run. Clusters consisting of compute nodes are managed via the Clusters tab under team settings.
* **Container:** Gradient runs Notebooks, etc., from Docker containers, which form a self-contained environment with defined software and versions, so that results are reproducible. When many containers are running, they are orchestrated using Kubernetes.
* **CORE vs. Gradient:** Paperspace CORE is our other main product besides Gradient, that provides virtual machines and compute power directly to users. It can be accessed from the GUI via the dropdown on the top left part of the screen.
* **GitHub:** GitHub is the most popular method online of managing versioning for software projects. Gradient is therefore integrated with it to provide version control for data science projects.
* **GPU:** Many machine learning compute operations such as dealing with large matrices (or tensors) run faster on a graphics card than a regular CPU processor. Paperspace is well-known for providing access to online GPU hardware that is cheaper and easier than trying to set it up for oneself. This is particularly useful for deep learning, or for large-scale work where distributed computing is needed.
* **GUI/CLI/SDK:** Gradient's 3 main interfaces are the graphical one, based in the browser (GUI), the command line one, typically accessed from the user's terminal (CLI), and the programmatic one, most commonly accessed from the user's code, typically Python (SDK).
* **Instances:** Gradient's compute power is supplied to the user in the form of instances. These can be CPU-based (C3, C5, etc.), or GPU-based (P4000, V100, A100, etc.), the latter generally named after the graphics card that they make available.
* **Metrics:** Metrics are arbitrary measurements that allow one to measure the performance of something, for example a machine learning model's predictions versus known ground truth. This means that they can provide direct quantitative proof of whether a business (or other) problem is being usefully solved. As such, they are given prominence in Gradient. Metrics can also be used for resource usage and application state.
* **ML Showcase:** Our [machine learning showcase](https://ml-showcase.paperspace.com/projects) provides an easy route to try out contributed data science projects and analyses in Gradient, currently via Notebooks.
* **Public Datasets:** There are many 1000s of datasets online, often in hard-to-navigate or slow-to-download-from locations. Our [curated set of public datasets](https://docs.paperspace.com/gradient/data/data-overview/private-datasets-repository/public-datasets-repository) provides a convenient starting point for users who want to learn-by-doing by writing their own analyses.
* **SAML/SSO:** This is a method of authentication that is more secure than usernames and passwords, and can be useful for teams in enterprise environments.
* **Team:** Gradient allows groups of users to have access to the same set of projects, and hence work as a team. This is useful for collaboration on large projects, or simply when it is useful for one's work to be visible to colleagues.
* **Versioning:** Many objects in Gradient are versioned, e.g., Datasets, Models, and Workflows. Versions are denoted by unique IDs, for example a Dataset can have an ID for the overall dataset, and a multiple versions, as in `abc123def456ghi:jklmno`, the versions being after the colon. Sometimes IDs need to be referred to directly, but often more convenient designations can be used, such as a name for a Dataset instead of its ID.

For more concepts, and context in which they are used, see the rest of this documentation, or our [AI Wiki](https://docs.paperspace.com/machine-learning/).
