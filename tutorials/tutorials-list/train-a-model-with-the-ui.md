# Train a Model with the Web UI

### **Objectives**

* Explore Gradient Projects
* Learn the workflow involved in training a model
* Use custom containers with jobs
* Create an Experiment that trains a Scikit-learn model
* Share files and models across jobs

## **Introduction**

In this tutorial, we’ll show you how to train a linear regression model to predict the salary of a software engineer depending on their experience. The dataset is partially based on the [Stack Overflow salary calculator](https://stackoverflow.com/company/salary), which we’ll use to build a single variate linear regression model with one feature \(experience\) and label \(salary\).

The Experiment generates a Python pickle file that gets stored in the shared storage service of Gradient.

## **Create a Project and an Experiment for Training the model**

After signing in, click on Gradient in the navigation bar on the left to choose Projects. Click on the Create Project button and select Create Standalone Project. Enter a name for the project when prompted.

![Create a new project via Projects &amp;gt; Create a Project](../../.gitbook/assets/screen-shot-2021-01-18-at-8.47.38-pm%20%281%29%20%281%29.png)

## Creating the Experiment

Within this project, we will create an experiment that trains the model.

![Create an experiment from within the project itself. We can use the CLI or the experiment builder](../../.gitbook/assets/screen-shot-2021-01-18-at-9.18.37-pm.png)

Experiment Builder is a wizard-style UI tool to submit a job.

The first step is to choose a machine type for scheduling the Experiment. Gradient takes advantage of Google Compute Engine’s preemptible instances to provide low-cost infrastructure. Make sure you check  **Enable low-cost instances**. Choose G1 machine type that comes with 1 CPU core, 1.7GB RAM, and 250GB SDD. This configuration is sufficient for the Scikit-learn training job. For TensorFlow and PyTorch, you can select a GPU-based machine type for accelerating the job.

![](https://camo.githubusercontent.com/743a7881fbf7e75aae721624c78f6be01de29bc5/68747470733a2f2f6c68352e676f6f676c6575736572636f6e74656e742e636f6d2f666641796a413950534e337a2d533779654435637369683446426851414958437a626b6c6571656549527958474b73544d7a6f326133543933485559703859464e31586169574b36707543634b4a454d64696f69447662622d75695931367a63666679685635774e4b4678467337574253513469334959586256776476516b577443396a49354e69)

In Gradient, Experiments are based on a container image that provides the runtime and dependencies. For this tutorial, we are using an image that contains Python 3 runtime with Scikit-learn framework.

![](https://camo.githubusercontent.com/6275444f75eb05108d20e2b3b8cc218709384ab4/68747470733a2f2f6c68352e676f6f676c6575736572636f6e74656e742e636f6d2f366e30456638425942737457574b7070697452416d4b776d695a78493137494b7863526562756e6d757a5578476c394f5141474a4e4e746853586f4a6876487957694a6f6554767a4b5f74786b5f74596f314d6a3358525f764c326864384147427558325a4f5f2d633455565851364a5074596a5844514b6331626b474b635f6a7a794d77644444)

On a side note, if you want to use your own container image, feel free to use or modify the Dockerfile and push it to a public container registry such as Docker Hub.

```bash
FROM alpine:latest

LABEL MAINTAINER="Janakiram MSV <janakiramm@gmail.com>"

# Linking of locale.h as xlocale.h
# This is done to ensure successfull install of python numpy package
# see https://forum.alpinelinux.org/comment/690#comment-690 for more information.

WORKDIR /var/www/

ENV PACKAGES="\
    dumb-init \
    musl \
    libc6-compat \
    linux-headers \
    build-base \
    bash \
    git \
    ca-certificates \
    freetype \
    libgfortran \
    libgcc \
    libstdc++ \
    openblas \
    tcl \
    tk \
    libssl1.0 \
    "

ENV PYTHON_PACKAGES="\
    numpy \
    matplotlib \
    scipy \
    scikit-learn \
    pandas \
    nltk \
    "

RUN apk add --no-cache --virtual build-dependencies python3 \
    && apk add --virtual build-runtime \
    build-base python3-dev openblas-dev freetype-dev pkgconfig gfortran \
    && ln -s /usr/include/locale.h /usr/include/xlocale.h \
    && python3 -m ensurepip \
    && rm -r /usr/lib/python*/ensurepip \
    && pip3 install --upgrade pip setuptools \
    && ln -sf /usr/bin/python3 /usr/bin/python \
    && ln -sf pip3 /usr/bin/pip \
    && rm -r /root/.cache \
    && pip install --no-cache-dir $PYTHON_PACKAGES \
    && apk del build-runtime \
    && apk add --no-cache --virtual build-dependencies $PACKAGES \
    && rm -rf /var/cache/apk/*
```

With the runtime container in place, we now need to point Gradient to the dataset and the training script. This is done through the integration with GitHub. Gradient pulls the GitHub repo into the experiment workspace and uses the assets for the training job.

Feel free to explore the [GitHub repo](https://github.com/janakiramm/Salary.git) that contains the dataset along with the code for training and deployment.

Let’s point Gradient to the tutorial repo on GitHub.

![](https://camo.githubusercontent.com/beb439ed3f8d715a2c2476754cc1d0a68aee1d40/68747470733a2f2f6c68362e676f6f676c6575736572636f6e74656e742e636f6d2f4879684a312d31703030504f424b74734734626c3161784b6359514f437a38383043525672644453396738327162392d70745379445969747461584f48737478726169575a643359634e6c717755556779414f75663361544a5933626972584a4d6a58594b75736d654d496651584941766c323948586a7552484156706d376f6d54723659383278)

Finally, let’s define the command for the job which is the Python script that executes within the context of the runtime of the container. When the script exits gracefully, the job is marked as complete.

The command for this job is `python train/train.py -i ./data/sal.csv -o /storage/salary`. The script, `train.py`, takes the source location of the dataset \(`sal.csv`\) and the target location to save the training model \(`/storage/salary)`.

In Gradient, any file that is saved at `/storage` location becomes available to other jobs and experiments. By persisting the model to this location, we will be able to access it later.

![](https://camo.githubusercontent.com/4d706f3814c25137ff06a776bbc3aa8a6043cde5/68747470733a2f2f6c68342e676f6f676c6575736572636f6e74656e742e636f6d2f754d6935564348524d2d624970764d724d306c70466356536277544934713379314a64496b35775f6c3038686730654b794863614f76556c6143744967396f54616d494567583771334a5735647233466552365957353447645f4a4c4d5f304e4470484c56555f72377742662d3350327861735a364d54497541396b41696334687356626775454f)

We are now ready to kick off the training job by clicking on the _Submit Experiment_ button.

Gradient adds the job to the queue and schedules it in one of the chosen machine types. In a few minutes, the job execution completes.

You can verify the logs that show the coefficients like Mean Square Error \(MSE\), Intercept, and Slope printed to the stdout in the code.

Feel free to explore the environment and files section of the job.

![](https://camo.githubusercontent.com/f53f213a488d07b9f8f5b80263ee339bac4937a5/68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f587473744f544e3148447054712d454f4463443467396953797054373056755f79684354594149646561306334694b4730715a6e435f586b6a58315941455063483858686d4b62527279474d4e4967686e326d355656335666385a3266327342596f744c326a3853446f73725a78694552635a47595f57796c444a4a556c525f5f47503133774c51)

The fully trained and pickled model \(`model.pkl`\) is now available at `/storage/salary` location. You can now safely delete the job to clean up the project.

