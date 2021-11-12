# End-to-End Sample Project: Deep Learning Recommender with TensorFlow

This tutorial shows by example how to use Gradient Notebooks and Workflows, and the interaction between them. The project is an end-to-end demonstration of building a recommender system then adding deep learning to it.

Many real data science projects begin with an exploratory phase where the data are investigated and machine learning models trained, then if value is found the team wishes to put the model into production. While it is not a requirement to be the case, often the exploratory phase will correspond to using Notebooks, and the production (or production-like) phase to using Workflows.

Many online demonstrations also either focus on the model, neglecting the data preparation and deployment into production, or they focus on the engineering and neglect the data science. Here, we show both.

**Tutorial contents**

The tutorial consists of

* A self-contained [**Notebook**](https://github.com/gradient-ai/Deep-Learning-Recommender-TF/blob/main/deep\_learning\_recommender\_tf.ipynb) that presents the project end-to-end. We include extensive commentary so that the reader can follow along without having to refer to other material.
* Two Workflow specs, [workflow-train-model.yaml](https://github.com/gradient-ai/Deep-Learning-Recommender-TF/blob/main/workflow-train-model.yaml) and [workflow-deploy-model.yaml](https://github.com/gradient-ai/Deep-Learning-Recommender-TF/blob/main/workflow-deploy-model.yaml), that are called by the Notebook, to train and deploy the model respectively.
* A [**GitHub repository**](https://github.com/gradient-ai/Deep-Learning-Recommender-TF), containing the Notebook, Workflows, and other files.
* Accompanying 6-part blog series entitled [**End-to-End Recommender System with Gradient**](https://blog.paperspace.com/end-to-end-recommender-system-part-1-business-problem/), that explains the project end-to-end in a manner accessible to a broader readership.

**Running the Tutorial**

Assuming you are [signed up for Gradient](https://console.paperspace.com/signup?gradient=true) and [logged in](https://docs.paperspace.com/gradient/get-started/quick-start#logging-in-for-the-first-time), to run the tutorial, run the Notebook. To do this using Gradient:

* In the Gradient GUI, create a Project with a name, e.g., Deep Learning Recommender
* Within the project, create a Notebook with the following settings:
  * Don't select any of the boxes under Select a runtime
  * Select a machine = C4 (C5, P4000, etc., will also work)
  * Public/private = set to preferred option
  * Under Advanced options:
    * Set the Workspace URL field to `https://github.com/gradient-ai/Deep-Learning-Recommender-TF` to point to this repository.
    * Set the Container name field to `tensorflow/tensorflow:2.4.1-gpu-jupyter`
    * Set the Container command to `jupyter notebook --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.trust_xheaders=True --NotebookApp.disable_check_xsrf=False --NotebookApp.allow_remote_access=True --NotebookApp.allow_origin='*'`
    * The other options can remain the same.
* Start the Notebook
* Once the Notebook has started, click`deep_learning_recommender_tf.ipynb` to run in the usual way by clicking `Run` under each cell in turn.

Notebook creation can also be done on the command line if desired, via `gradient notebooks create`. For more details on Notebooks, see the [documentation](https://docs.paperspace.com/gradient/explore-train-deploy/notebooks).

_Workflow_

To run the Workflow section of the Notebook, section 4.3, requires some extra steps. These are detailed in the Notebook.

**Target Audience**

We assume the readers of the tutorial are generally technical, but are not necessarily experts in data science, engineering, recommender systems, or Gradient.
