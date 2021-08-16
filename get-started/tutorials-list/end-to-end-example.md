# End-to-end example: Deep Learning Recommenders in TensorFlow

This tutorial shows by example how to use Gradient Notebooks and Workflows, and the interaction between them. The project is an end-to-end demonstration of building a recommender system then adding deep learning to it.

Many real data science projects begin with an exploratory phase where the data are investigated and machine learning models trained, then if value is found the team wishes to put the model into production. While it is not a requirement to be the case, often the exploratory phase will correspond to using Notebooks, and the production \(or production-like\) phase to using Workflows.

Many online demonstrations also either focus on the model, neglecting the data preparation and deployment into production, or they focus on the engineering and neglect the data science. Here, we show both.

**Tutorial contents**

The tutorial consists of

* A self-contained [**Notebook**](https://github.com/gradient-ai/Deep-Learning-Recommender-TF/blob/main/deep_learning_recommender_tf.ipynb) that presents the project end-to-end. We include extensive commentary so that the reader can follow along without having to refer to other material.
* Two **Workflows** that are called by the Notebook, to train and deploy the model respectively.

  [**GitHub repository**](https://github.com/gradient-ai/Deep-Learning-Recommender-TF), containing the Notebook, Workflows, and other files.

* Accompanying 6-part blog series \(coming soon!\) on the [**Paperspace blog**](https://blog.paperspace.com), that explains the project end-to-end in a manner accessible to a broader readership.

**Running the Tutorial**

Assuming you are [signed up for Gradient](https://console.paperspace.com/signup?gradient=true) and [logged in](https://docs.paperspace.com/gradient/get-started/quick-start#logging-in-for-the-first-time), to run the tutorial, run the Notebook. To do this using Gradient:

* In the Gradient GUI, create a Notebook with the following settings:
  * Name = Deep Learning Recommender \(or any allowed name\)
  * Select a runtime = TensorFlow 2.4.1
  * Select a machine = C5 or P4000
  * Public/private = set to preferred option
  * Under Advanced options, change the Workspace URL field from `https://github.com/gradient-ai/TF2.4.1.git` to `https://github.com/gradient-ai/Deep-Learning-Recommender-TF` to point to this repository. The other options can remain the same.
  * Start the Notebook
* Once the Notebook has started, click`deep_learning_recommender_tf.ipynb` to run in the usual way by clicking `Run` under each cell in turn.

Notebook creation can also be done on the command line if desired, via `gradient notebooks create`. For more details on Notebooks, see the [documentation](https://docs.paperspace.com/gradient/explore-train-deploy/notebooks).

_Workflow_

To run the Workflow section of the Notebook, section 4.3, requires some extra steps. These are detailed in the Notebook.

**Target Audience**

We assume the readers of the tutorial are generally technical, but are not necessarily experts in data science, engineering, recommender systems, or Gradient.

