---
description: >-
  Welcome to Gradient Notebooks! In this tutorial we'll cover everything you
  need to know to start using notebooks backed by powerful free and paid GPU
  instances.
---

# Gradient Notebooks Tutorial

## **Introduction**

[Gradient Notebooks](https://www.gradient.run/notebooks) is a web-based Jupyter IDE with high-powered GPUs. During this tutorial, we will learn to create and run new Gradient Notebooks by using a pre-built runtime from Paperspace and by bringing our own files and container with advanced options.

![Create your first Gradient Notebook to get up and running with a real ML project on a high-powered GPU.](<../../.gitbook/assets/create notebook intro dark.gif>)

If you have experience running [Jupyter](https://jupyter.org/try) Notebooks or [JupyterLab](https://pypi.org/project/jupyterlab/) on other managed cloud services (or on your local machine), you will find that Gradient Notebooks combines the functionality of Jupyter with an additional set of powerful features:

* Persistent storage
* Generous free-tier CPU and GPU instances
* Powerful paid-tier CPU and GPU instances
* Unlimited duration runtimes for paid instances
* Run on a pre-configured template or your own custom Docker image&#x20;

As a result, Gradient Notebooks is one of the most popular managed notebook services available today and is in use by hundreds of thousands of developers around the world.

## Why start with Gradient Notebooks?

Notebooks are an [increasingly popular](https://storage.googleapis.com/kaggle-media/surveys/Kaggle's%20State%20of%20Machine%20Learning%20and%20Data%20Science%202021.pdf) abstraction in machine learning. Notebooks eliminate many of the tooling headaches associated with creating a development environment for ML and are useful for establishing a development environment that is both reproducible and collaborative.

Yet notebooks are not for everybody. It's common for a data scientist and a machine learning engineer to have divergent views on the usefulness of a notebook. That's perfectly OK.&#x20;

Gradient Notebooks is designed to be the simplest entry point into Gradient but it's not the only one. If you're more interested in MLOps capabilities enabled by [Gradient Workflows](workflows-sample-project-stylegan2/) or [Gradient Deployments](broken-reference), we invite you to skip ahead to those tutorials.&#x20;

Meanwhile, if you don't know where to start -- start with Gradient Notebooks. There's no faster way to begin building a powerful ML application than within the friendly confines of a GPU-backed notebook. We'll aim to demonstrate that fact to you right here in this tutorial.

Let's get started.

## **Setting up our first notebook to run Fast.ai**

In the first part of this tutorial, we will create a Gradient Notebook to run the latest version of the popular [Practical Deep Learning for Coders](https://course.fast.ai) course from [Fast.ai](https://www.fast.ai).

To start, we'll need to create a Gradient Project if we haven't done so already. For the sake of this tutorial we've named our project `Fast.ai: Practical Deep Learning for Coders`. Later on we'll change the name of our project when we add a second notebook.

### Creating the notebook

While in our new project, let's tab over to the `Notebooks` tab and select the button that says `Create` .

![The Notebooks tab within a new project will urge us to create a new notebook.](<../../.gitbook/assets/create notebook dark.png>)

Each time we create a notebook, we'll be prompted to configure a few options. In the first part of this tutorial, we'll select a runtime and a machine. Later on we'll get more advanced during this phase but for now we're going to use a prebuilt runtime that Gradient provides directly in the console.

![In the first part of this tutorial we'll select the fast.ai runtime.](<../../.gitbook/assets/select fastai dark.gif>)

We'll be selecting the `Paperspace + Fast.ai` runtime to start. We'll explain what exactly this means in the second part of the tutorial.&#x20;

For now, we just need to understand that we are instructing Gradient to copy the contents of a special fast.ai repository (which contain the fast.ai exercise files)over to our new notebook and to run those files on a compute instance pre-installed with compatible dependencies.

### **Selecting the machine and launching the new notebook**

We will now select the machine or instance on which we would like to run the notebook. We have a number of options to run our first notebook, including `Free-CPU` and `Free-GPU` instances. In this tutorial we'll be using the `Free-GPU` instance as much as possible -- however if you have already upgraded your Gradient subscription and would like to use more advanced instances like `Free-P5000` or `Free-RTX4000` (or even a paid instance like `V100`) please go ahead!

![We'll select a Free-GPU instance. We can also upgrade our subscription at any time to unlock more powerful GPU instances.](<../../.gitbook/assets/select machine dark.png>)

For now we'll select the `Free-GPU` machine because it is available and we don't need a high-powered GPU here. Let's then go ahead and start our notebook.

### The Gradient Notebooks IDE

After we create the notebook, we should see the Gradient Notebooks IDE. It can take a minute for the notebook to load, so keep an eye on the status bar.

![The status bar lets us know the state of the notebook. Other states include Running, Saving, and Offline.](<../../.gitbook/assets/setting up instance dark.gif>)

Once the notebook is in the `Running` state we'll see something like this:

![Now that the status bar reads Running, we know that our notebook is ready to use.](<../../.gitbook/assets/notebook started dark.png>)

We are officially up and running! Our notebook can now run and execute commands.

As we start to run commands, let's keep an eye on the the bottom bar of the IDE which provides some useful information and metrics. Whenever we want to know if our instance is "doing something" we can look to the bottom bar to see what's going on with our machine.

![The bottom bar of the console IDE will give us a good sense of how our compute instance is performing. This image shows an idle notebook that is not running any commands and therefore has low utilization.](<../../.gitbook/assets/status bar dark.png>)

We will now begin to run cells from the file called `01_intro.ipynb`. We should see the cell executing like so:

![You can run a single cell within a notebook by selecting the Run button. The Run All button (top right of the IDE) is another option.](<../../.gitbook/assets/run notebook dark.gif>)

We were able to run our first cell, but perhaps we want to have our `!pip install` statements in their own cell? That's easy! First we'll cut the `!pip install` command from the existing cell, then we'll use the `+` button, we'll select `Insert Code`, and then we'll paste the `pip` command into the newly created cell.&#x20;

![We can create a new code or markdown cell by using the + button that appears when we hover over a cell.](<../../.gitbook/assets/add cell dark.gif>)

You may have also noticed that you can select `Insert Markdown`, which comes in handy when you want to add an explanatory or reference block of text to your ipynb file.

We should note that Gradient Notebooks supports editing standard code files as well with full autosave capabilities. In this image we are modifying the contents of the `requirements.txt` file that ships with the fast.ai learning materials:

![We can also edit non-ipynb files within the Gradient Notebooks IDE. Here we modify  a requirements.txt file.](<../../.gitbook/assets/otherfiles dark.png>)

Great! At this point we recommend that you run through as many of the fast.ai files and cells that you care to run. It is a fantastic course written by some of the best ML educators on the planet and we can't recommend it more strongly.

Your notebook will run for up to 6 hours on a free instance. If you'd like to enable infinite runtimes or faster GPU instances, you will need to upgrade your [Gradient subscription](https://gradient.run/pricing) and recreate the notebook. Meanwhile you can run as many 6-hour sessions on free instances as you like provided Gradient has capacity. The free GPU instances tend to be extremely popular so you may need to play around with your timing to secure a free GPU instance during peak usage hours.

### Stopping the notebook

When it's time to stop the notebook, we can let the auto-shutdown timer expire or we can also shut down the instance manually via the instance panel in the sidebar (depicted below) or via the `Stop Instance` button in the top status bar.

![One way we may stop the instance manually is from the instance selector in the sidebar. ](<../../.gitbook/assets/stop instance dark.gif>)

If we do _not_ stop the instance manually, the auto-shutdown timer will turn off the `Free-GPU` instance at the 6-hour mark. Paid instances will auto-shutdown if an auto-shutdown interval has been specified. The default is 12 hours for paid instances.

## Setting up our second notebook and running CLIP-PixelDraw

Now that we understand how to set up a basic notebook in Gradient, let's try a more advanced notebook configuration. Our goal this time around will be to use [CLIP and PixelDraw](https://github.com/gradient-ai/ClipIt-PixelDraw) to generate an imaginative clip-art piece from a string of text that we will input.&#x20;

Before we start, if we are on the Gradient free tier, we'll need to [stop the notebook instance](gradient-notebooks-tutorial.md#stopping-the-notebook) that we launched in the first example so as not to exceed the limit of QTY 1 concurrent running notebooks on the free plan. If we have upgraded our Gradient account, we can ignore this step.

More information on Gradient tier limits is available [here](https://gradient.run/pricing) under `Compare Plans`.

### Create a new notebook

Let's return to the Gradient console and give our project a more descriptive name since we'll be adding a second notebook to it:

![Here we're renaming our project in the Gradient console to better reflect the contents which will soon be two different notebooks.](<../../.gitbook/assets/rename project dark.gif>)

Next let's go ahead and select `Create` to again bring up the `Create a notebook` screen:

![As we create our second notebook, we'll learn a little bit more about runtimes.](<../../.gitbook/assets/second notebook create dark.gif>)

As the animation above suggests, this time we've called attention to the large number of runtimes that are available to us if we swap over from `Recommended` to `All` in the runtime selector. Gradient frequently adds support for new runtimes. The console is therefore a great place to come and learn about new libraries and technologies.

We're taking a look at all these runtimes now because we need to understand what a runtime _actually is_ before we can create and launch our own custom runtime.&#x20;

![Selecting All in the runtime selector reveals a large number of prebuilt runtimes available on Gradient.](<../../.gitbook/assets/All tiles runtime selector dark.png>)

### What is a runtime?

In Gradient, a runtime is a specific combination of a workspace, which is pulled from a git repository via something like GitHub, and a container, which is pulled from a container registry via something like DockerHub.&#x20;

To visualize this, let's first toggle the tile called `Transformers + NLP` from [Hugging Face](https://huggingface.co).

![We're going to select the Transformers + NLP tile in the console to understand what a runtime is.](<../../.gitbook/assets/hugging face tile dark.png>)

Now let's scroll down to the `Advanced Options` slider at the bottom of screen and toggle it on. We will see these fields available in the advanced options:

![Workspace and Container parameters are available in the Advanced options section after enabling the toggle.](<../../.gitbook/assets/advanced options dark.png>)

This particular Hugging Face tile is specifying `Workspace URL`, `Container Name`, and `Command`.

* `Workspace URL`: URL of the GitHub repository that we wish Gradient to clone into this notebook
* `Container Name`: Location of the image on [Docker Hub](https://hub.docker.com) that we would like Gradient to load into this notebook
* `Command` _(Advanced)_: Bash command that we want to pass to the Jupyter kernel on instantiation

Thus a runtime is simply a combination of `Workspace URL` and `Container Name` that results in some files from a repo running against a container image. Pretty simple!

Now let's go ahead and create a notebook with a custom runtime.&#x20;

### What we're trying to accomplish in this notebook

For this notebook we'll be using an implementation of [CLIP](https://openai.com/blog/clip/) from OpenAI which allows us to create synthetic artwork from a text prompt that we ourselves input.

In this demo implementation we'll use a text prompt from [one of our favorite books](https://en.wikipedia.org/wiki/Dune\_\(novel\)) (and now a major Hollywood film) and we'll see what the image generator can come up with in response.&#x20;

Pretty cool! Let's get started.

### Using custom runtime parameters to create a notebook

First we need to build our notebook. But _instead_ of using a prebuilt runtime tile, we're going to ignore the tiles and go right for the instance type. Let's select the highest GPU instance that we have available.&#x20;

Next, we're going to toggle the `Advanced options` and enter the following parameters:

* `Workspace URL`: [https://github.com/gradient-ai/ClipIt-PixelDraw.git](https://github.com/gradient-ai/ClipIt-PixelDraw.git)
* `Container Name`: paperspace/clip-pixeldraw:jupyter

In this case we are using a workspace that contains a number of files related to this generative art project and we're using a container that has a number of libraries pre-installed to make our job as easy as possible.

Many advanced Gradient Notebooks users will bring their own repositories and containers into notebooks. We'll take a look at what this means after we get this second notebook up and running.

For now, our advanced options should look like this:

![Make sure to copy and paste the locations of the workspace and the container in the Advanced options section of the Create a notebook workflow.](<../../.gitbook/assets/advanced options CLIP dark.png>)

Once we're satisfied with the parameters, let's go ahead and start the notebook! Once the notebook is initialized, it will look something like this:

![Running the CLIP-PixelDraw notebook.](<../../.gitbook/assets/running CLIP dark.png>)

Let's go ahead and run the trio of `!git clone` commands at the top of the notebook at this time:

![Start the !git clone commands to pull down additional required packages.](<../../.gitbook/assets/start CLIP dark.gif>)

The next thing we're going to do is look at the prompt we're using in the `pixeldraw.py` file. By default that prompt is set to the following:

```
Paperspace.com helps you do machine learning #pixelart
```

We're going to go ahead and change that. We can change the sentence to anything we like. In the animation below, we'll change the prompt to something that reminds us the sand-covered planet from Dune:

```
On the desert planet of Arrakis, the spice must flow!
```

![Changing the default prompt of the generator to a sentence of our choosing.](<../../.gitbook/assets/clipit prompt dark.gif>)

Next, we'll head back over to the .ipynb file and we'll run the cell that contains the following:

```
!python pixeldraw.py
from IPython.display import Image
Image(filename='output.png')
```

This is going to run the code that we just modified in `pixeldraw.py`.&#x20;

Depending on what GPU instance you are using, this can take anywhere from 8 minutes - 20 minutes. So be careful! You may be waiting for a while.

![It can take a while for a clip-art piece to generate while using CLIP but the results are usually worth it.](<../../.gitbook/assets/clipit loading dark.gif>)

After all that waiting, we are able to generate a surprisingly complex scene with some sophisticated imagery:

![The clip-art we generated in response to the prompt: On the desert planet of Arrakis, the spice must flow!](../../.gitbook/assets/spice.png)

As we can see CLIP was able to interpret a desert setting, an ominous building, a mysterious person, and the object of the person's gaze -- some kind of container with something colorful inside of it and/or on top of it.&#x20;

Fantastic!

## What's next?

In this tutorial, we first created a basic Gradient Notebook from a recommended runtime tile in the console. This first notebook, which contained the course materials from [fast.ai](https://www.fast.ai), helped us see how easy it is to get up and running on a powerful (and free) GPU instance in Gradient Notebooks.&#x20;

Next, we created a second notebook -- this time by pulling a custom workspace from a GitHub repository and loading an image pre-loaded with dependencies from Docker Hub. This second notebook allowed us to create generative art with a simple text prompt. It also demonstrated how easy it is to bring external code and containers into Gradient Notebooks.

To take this tutorial further, we recommend that you specify a repository to clone or a container to pull on your own. For example, let's say we were browsing [Papers with Code](https://www.paperswithcode.com) and we stumbled upon a really cool [new implementation of CLIP](https://paperswithcode.com/paper/styleclipdraw-coupling-content-and-style-in) that uses a different artistic technique to generate artwork. To try it out we could create a new notebook with `Workspace URL` in `Advanced options` set to:

```
https://github.com/pschaldenbrand/styleclipdraw
```

This would pull the target files into an instance running the default Gradient container.

The next step after that would be to fork the repository to a new public or private repo and modify it. We could also create our own Docker container pre-loaded with new dependencies and submit that to a public or private registry.&#x20;

The ability to create new repos/containers from existing resources in Gradient is extremely powerful. The same could be said for building a repo that that someone else can pull or a container that someone else can build.

One common pathway for advanced users is to start with something simple like pulling a repo of interest and to build complexity up over time.

If you need inspiration, the [Paperspace blog](https://blog.paperspace.com) is filled with novel implementations that often include code and demo notebooks. We've also included a list of additional references below.

If you have any questions, you can reach us any time at **hello@paperspace.com** or [@hellopaperspace](https://twitter.com/hellopaperspace).&#x20;

## Reference reading

* Browse a collection of starter notebooks created for Gradient called [ML Showcase](https://ml-showcase.paperspace.com)
* Learn more about [custom notebook containers](../../explore-train-deploy/notebooks/create-a-notebook/notebook-containers/building-a-custom-container.md)
* Learn more about [instance types](../../more/instance-types/), including [free tier](../../more/instance-types/free-instances.md) instances
* Learn more about [persistent storage](../../more/overview/billing-and-subscriptions/notebooks-storage.md) which is automatically mounted at `/storage`

## Additional tutorials

* Gradient Workflows
* Gradient Deployments
