# Workflows Sample Project: NLP Text Generator

This is our NLP Text Generation Tutorial example, which we consider to be **intermediate level** in our tutorials range. It runs the GPT-2 model from HuggingFace: [https://huggingface.co/gpt2](https://huggingface.co/gpt2) . The corresponding Git repository is at [https://github.com/gradient-ai/NLP-Text-Generation](https://github.com/gradient-ai/NLP-Text-Generation) .

The example shows a short Workflow that is quick to run, with the primary aim of helping you to quickly get going with Gradient repo-linked projects with a modern use case. It includes:

* Text generation from a modern deep-learning-based natural language processing model, GPT-2
* Gradient Projects linked to GitHub repositories
* Gradient Workflows
* Triggering a Workflow to rerun based upon a change in the repository, as needed in many production systems
* Versioned Gradient-managed Datasets as output

The repo contains 2 files: `nlp_text_generation.py` in the main directory, and `nlp_text_generation.yaml`in the `.gradient/workflows` directory. The YAML file contains the Gradient Workflow which in turn calls the Python script.

The Workflow is triggered to run when the YAML file is present in the `.gradient/workflows/` directory, and the repo is linked to the user's Gradient project. The Workflow clones this repo and then in turn calls the Python script. The script outputs the generated text to the file `outputs.txt` in the Gradient-managed Dataset `demo-dataset`, which the user can then view.

The Workflow runs on the Paperspace HuggingFace NLP container \(`paperspace/transformers-gpu:0.4.0`\).

### Steps to run this tutorial

_Easiest way: clone the example repository_

Assuming you are [up and running with Gradient](https://docs.paperspace.com/gradient/get-started/quick-start), and have the **GitHub app** installed to your GitHub username, this Project runs as a sample repository.

* [Create a Project](https://docs.paperspace.com/gradient/get-started/quick-start#first-create-a-project)
* Under the Workflows tab of the Project, click Create a Workflow
* In the illustrated list of Projects in the central panel, select the one for "NLP Text Generation"
* Select your GitHub username from the Account and Organizations dropdown list
* Choose a repository name
* Click "Create Project"

The Workflow will then run.

_Alternative method: create your own repo fork first_

You can also fork your own copy of this tutorial repo, then create a repo-linked Workflow that points to the fork:

* Navigate to [https://github.com/gradient-ai/NLP-Text-Generation](https://github.com/gradient-ai/NLP-Text-Generation) in your browser
* In the resulting GitHub GUI page, click "Fork" in the top right
* Follow the usual GitHub procedure by selecting your GitHub account to fork the repo to
* [Create a Project](https://docs.paperspace.com/gradient/get-started/quick-start#first-create-a-project)
* Under the Workflows tab of the Project, click Create a Workflow
* Instead of selecting the sample repo for "NLP Text Generation", click "import an existing gradient repository"
* Choose the repo fork you just created from the dropdown list
* This will take you to the "Let's create a Workflow" screen. Change any of the files in your forked repo to trigger the `nlp_text_generation.yaml` file under `.gradient/workflows/` to run. For example, add a few characters to the `README.md`.

The result should be the same as above.

_Note_: When running the Workflow from a project linked to your own fork of the repo, it will still be cloning from the original location [https://github.com/gradient-ai/NLP-Text-Generation](https://github.com/gradient-ai/NLP-Text-Generation), unless you choose to alter the location that the Workflow points to, which is optional.

#### Altering the model settings and triggering a Workflow rerun

The ability to trigger Workflow reruns is useful in several situations, especially more MLOps and production-oriented ones where the state of the collection of code, data, deployments, models, and other components should be consistent.

Here, changing the model settings can be used to trigger a rerun of the model. The 4 values under "Settings" in the `nlp_text_generation.py` script \(random seed, maximum text length, number of returned text sequences, and the initial text sentence\) can be altered to generate different text.

If the resulting updated version of the `nlp_text_generation.py` file is uploaded to the repo main directory to replace the one present, and the project remains linked to the repo, the Workflow will be rerun. A new `output.txt` file is generated, and placed in a new version of the output Gradient-managed Dataset.

### Next Steps

This tutorial's primary purpose is to show repo-linked projects, via a relevant modern use case of text generation. For longer end-to-end examples of Workflows in Gradient, see the [Recommender](https://docs.paperspace.com/gradient/get-started/tutorials-list/end-to-end-example) and [StyleGAN2](https://docs.paperspace.com/gradient/get-started/tutorials-list/workflows-sample-project) tutorials. Recommender has a Notebook, Workflow, deployment, and non-repo-linked project. StyleGAN2 is repo-linked and shows data preparation, model training, and model inference.

The flexible interface provided by the HuggingFace models means that the Python code shown in `nlp_text_generation.py` can be altered to use other NLP models by altering the `generator = pipeline('text-generation', model='gpt2')`line that points to the model, and the `generator()` function line to pass the right arguments. For example, the GPT-Neo series at [https://huggingface.co/EleutherAI](https://huggingface.co/EleutherAI) can be run. Some of these, at 5GB or 10GB, are larger than the 548MB model that this tutorial downloads.

