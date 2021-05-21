# Workflows sample project: StyleGAN2

This sample project shows how to use Workflows to train a StyleGAN deep learning model to generate pictures of cats, based on the popular Nvidia [StyleGAN2](https://github.com/NVlabs/stylegan2) GitHub repository.

We assume the reader is familiar with the [basics of Workflows](https://docs.paperspace.com/gradient/explore-train-deploy/workflows), and here wishes to proceed to using them for real projects.

The code can be run by the user to create this project, or used as a starting point for another project.

### **Setup**

Assuming you are [signed up for Gradient](https://console.paperspace.com/signup?gradient=true) and [logged in](https://docs.paperspace.com/gradient/get-started/quick-start#logging-in-for-the-first-time), to get started, clone the [workflows sample project repo](https://github.com/gradient-ai/StyleGAN2-with-Workflows), which will give you the files `stylegan-2-download-and-extract-data.yaml` and  `stylegan2-train-and-evaluate-model.yaml`. These two YAML files specify the two workflows that make up this project, and can be run in the usual way that Gradient Workflows are run. The files are also shown [here](https://docs.paperspace.com/gradient/get-started/tutorials-list/workflows-sample-project/yaml-file-for-stylegan2-workflow) for reference.

Currently, the way to run Gradient Workflows is to use the command line interface \(CLI\), with a command like

```text
gradient workflows run \
  --id <your run ID> \
  --clusterId <your cluster ID> \
  --path ./stylegan2-train-and-evaluate-model.yaml \
  --apiKey <your API key>
```

This in turn requires you to

* [Create a project](https://docs.paperspace.com/gradient/get-started/managing-projects#create-a-project) and optionally [get its ID](https://docs.paperspace.com/gradient/get-started/managing-projects#get-your-projects-id)
* [Generate an API key](https://docs.paperspace.com/gradient/get-started/quick-start/install-the-cli#obtaining-an-api-key) for your project to allow access
* [Install the Gradient CLI ](https://docs.paperspace.com/gradient/get-started/quick-start/install-the-cli)on your machine
* Use or create a [Gradient Private cluster](https://docs.paperspace.com/gradient/gradient-private-cloud/about/setup/managed-installation) and [its ID](https://docs.paperspace.com/gradient/gradient-private-cloud/about/usage#finding-your-cluster-id)
* [Create the two workflows](https://docs.paperspace.com/gradient/explore-train-deploy/workflows/getting-started-with-workflows#creating-gradient-workflows) via CLI or GUI and [get their IDs](https://docs.paperspace.com/gradient/explore-train-deploy/workflows/getting-started-with-workflows#running-your-first-workflow-run)
* [Create output datasets](https://docs.paperspace.com/gradient/data/data-overview/private-datasets-repository#creating-a-dataset-and-dataset-version) for the two workflows
* [Import a placeholder file](https://docs.paperspace.com/gradient/data/data-overview/private-datasets-repository#creating-a-dataset-and-dataset-version) into each created output dataset

This is quite a lot of steps, and will simplify in the future as the Workflows product matures. \(See the caveats section below for more details.\)

Finally, you will need to edit the YAML to correspond to the IDs of your copies of the Gradient managed datasets that are output. This is because this is a production-grade MLOps system and everything must be versioned and specified exactly.

### Workflow time to run: Autoscaling

In the second workflow, `stylegan2-train-and-evaluate-model.yaml`, because it is training and evaluating a StyleGAN neural network, and our purpose here is to show a realistic example, it typically takes about an hour to run. The type of machine used can affect this quite significantly, so for best performance, you can use [autoscaling](https://docs.paperspace.com/gradient/gradient-private-cloud/about/setup/managed-installation#autoscaling-groups) with hot nodes enabled. With two each of C5, P4000, and V100, the resources specified in the YAML file are enabled and do not need to be spun up:

| Step number | Step name | Machine type |
| :--- | :--- | :--- |
| 1 | cloneStyleGAN2Repo | C5 |
| 2 | getPretrainedModel | C5 |
| 3 | evaluatePretrainedModel | V100 |
| 4 | generateImagesPretrainedModel | P4000 |
| 5 | trainOurModel | V100 |
| 6 | evaluateOurModel | V100 |
| 7 | generateImagesOurModel | P4000 |

We want two of each machine because steps 1 & 2, 3 & 5, and 4 & 7 can run in parallel, but 6 requires 5 to finish first. The generate images steps take less time than the evaluate and train steps, so they can be run using a P4000 machine, while V100 is best for steps 3, 5, and 6.

If you want to avoid complexity and use a simpler resource list, defaulting all steps to V100 will run in the same time, or it will run in 3-4 hours if all machines are P4000.

For a shorter runtime, see the sample workflow shown when creating a new workflow in the Gradient GUI.

### **What the workflow is doing**

The first workflow of the two downloads and extracts the data from [http://dl.yf.io/lsun/objects/cat.zip](http://dl.yf.io/lsun/objects/cat.zip) . The data is supplied as a 45 gigabyte .zip file, which we unzip into its LMDB database format, extract the WebP images it contains, and compile those images into the multi-resolution TFRecords format needed for training the model. Working with the large file demonstrates Workflows being used with realistic data sizes. The extract step subsamples the images to 1000, but this is controllable via the `--max_images` argument, and can be set to larger sample sizes at the expense of a longer training runtime in the second workflow.

The second workflow sets up the following steps, as shown in this directed acyclic graph \(DAG\) representation. The box colors show inputs, repo clone, pretrained model steps, and steps for our model. "Cat images subsample" is the set of extracted images from the first workflow.

![StyleGAN2 workflow. The gray boxes are inputs coming from outside the workflow.](../../../.gitbook/assets/image%20%2869%29.png)

We clone the StyleGAN2 repo, and get the online pretrained model. Then we use the repo's `run_metrics.py` to evaluate the pretrained model, and its `run_generator.py` to generate new cat images from it. At the same time \(Gradient Workflow jobs can run in parallel\), we train our model on some image data using `run_training.py`, then evaluate it and generate images from it in the same way as for the pretrained model. This allows us to compare the two models.

The DAG shows that, as one would expect, both models require the repo to be able to run, and then our evaluation requires our model to be trained first, but the pretrained evaluation does not.

To keep this tutorial tractable with a workflow runtime of hours and not days, we train on the small subsample mentioned above of the 1.6 million images available in the original dataset. So as we will see below, our model does not do well compared with the pretrained model. But to train the full model, the setup is the same as here: one would simply pass in the full-sized dataset and run for longer.

### Caveats

Gradient Workflows is still a new product \(beta stage\), and as such there are some caveats to this tutorial. All of these will go away as the Workflows product matures.

* _Requirement for Gradient private cluster:_ Current Workflows usage requires a Gradient private cluster. A public cluster for Workflows is being added to the Paperspace infrastructure that will remove this requirement.
* _Autoscaling:_ For best performance, autoscaling hot nodes can be configured. When using the public cluster, this will not be needed.
* _Invoke workflow from CLI only:_ Workflows must be invoked from the command line. In future, Workflows will be able to be invoked from CLI, SDK, or GUI, either manually, or automatically based on a trigger.
* _Create output datasets in GUI before running:_ Gradient managed datasets must be created before running a Workflow so that their IDs can be referenced. We plan that a new dataset ID will be able to be referenced in the workflow, and it will create the dataset if it does not exist.
* _Created dataset must contain placeholder file:_ Similarly, a newly created dataset must contain an imported file, e.g., a small text file as a placeholder. Otherwise the workflow will fail saying dataset cannot be referenced.
* _Workflows contain workaround code to avoid large files in their /output directories:_ We use the sequence gzip/split/cat/gunzip to break up the large files of images, extracted multi-resolution images in TFRecords format, and trained network, due to a machine memory usage issue. This is temporary, and gigabyte+ files will be able to be handled without needing this sequence. \(Files larger than machine memory will still need some kind of streaming, however, as one would expect.\)
* _Download data before running:_ The existing second part of the workflow, `stylegan2-train-and-evaluate-model.yaml`, can refer to a Gradient managed dataset, but a dataset containing that data is not yet public. So the user needs to run the first workflow, `stylegan-2-download-and-extract-data.yaml`, to enable their second workflow access the data. The public cluster will remove this requirement, and the user will be able to either run both workflows, or just run the second one and refer to our Gradient managed dataset containing the output from the first one.

### **Results**

If the workflow runs correctly, for the second workflow you will see a DAG that looks like this:

![DAG of second Workflow after a successful run of StyleGAN2](../../../.gitbook/assets/image%20%2876%29.png)

You can then explore in the usual way in the GUI the output logs of each job, the YAML, and the contents of the output directories. For the project here, this allows us to compare the results from our trained model to those from the pretrained one.

By viewing the output files of the `generateImagesPretrainedModel`, and `generateImagesOutputModel`          YAML jobs, we can see the quality of the images that the models generate. As expected, the pretrained model generates realistic looking cats:

![Generated cat from pretrained model](../../../.gitbook/assets/image%20%2813%29.png)

\(although looking closely some of them may have extra legs\), and in contrast, our trained model on only 1000 images clearly needs more time and data:

![](../../../.gitbook/assets/image%20%2859%29.png)

Some of its images have hints of a cat shape, but they are mostly noise. Again this is as expected.

To see a more quantitative comparison, in the output logs from the network evaluations, `evaluatePretrainedModel` and `evaluateOurModel`, the files `run.txt` contains the values for the `fid50k` and `ppl2_wend` metrics that we evaluated. `fid_50k` is the [Frechet Inception Distance](https://machinelearningmastery.com/how-to-implement-the-frechet-inception-distance-fid-from-scratch/), where lower is better, and 0 is perfect. `ppl2_wend` is the [Perceptual Path Length](https://towardsdatascience.com/explained-a-style-based-generator-architecture-for-gans-generating-and-tuning-realistic-6cb2be0f431#:~:text=Perceptual%20path%20length%20%E2%80%94%20measure%20the,that%20they%20might%20be%20entangled) in W, with path endpoints.

The difference between the models can be seen \(your result may vary slight from the numbers here\):

_Pretrained_

```text
stylegan2-cat-config-f time 44m 08s fid50k 35.4571
stylegan2-cat-config-f time 1h 16m 21s ppl2_wend 437.9006
```

_Ours_

```text
network-final time 45m 18s fid50k 386.3678
network-final time 1h 17m 42s ppl2_wend 19.5041
```

For our model, the `fid50k` is much higher, and the `ppl2_wend` much lower, both indicating a worse model.

The resolution to this is of course to train our model for longer \(days not hours\) on a training set of proper size, which is 10,000s images+, not 1000. The workflow and YAML setups are the same; we simply pass in the bigger image set.

### Future additions

As mentioned, Gradient Workflows is still a new product, and as such, aside from the caveats above, some of Gradient's functionality is also not yet supported. This includes

* Adding Gradient's multi-GPU support to Workflows
* Deployment, monitoring, and triggering model retraining
* GradientCI projects

Further YAML actions such as managed model creation \(as opposed to upload\), run a script, and managed deploy, are being added too.

Once these are available, the code here will be straightforwardly alterable or extensible to take advantage of them.

