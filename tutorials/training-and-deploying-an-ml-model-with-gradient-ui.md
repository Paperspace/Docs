# Train & Deploy an ML Model with the Experiment Builder

## **Objectives**

* Explore Gradient Projects
* Learn the workflow involved in training a model
* Use custom containers with jobs
* Create a job that trains a Scikit-learn model
* Share files and models across jobs
* Create a long-running job \(web service\) that serves the model
* Access the REST endpoint exposed by a job

## **Introduction**

In this tutorial, we’ll show you how to train a linear regression model to predict the salary of a software engineer depending on their experience. The dataset is partially based on the [Stack Overflow salary calculator](https://stackoverflow.com/company/salary), which we’ll use to build a single variate linear regression model with one feature \(experience\) and label \(salary\).

There are two jobs involved in this workflow—training and deploying. The first job generates a Python pickle file that gets stored in the shared storage service of Gradient. The same pickle file will be used by the second job running a Flask web server to expose a REST endpoint. This job will serve the model through the inferencing endpoint.

## **Create a Project and an Experiment for Training the model**

After signing in, click on Gradient in the navigation bar on the left to choose Projects. Click on the Create Project button and select Create Standalone Project. Enter a name for the project when prompted.

![](https://lh3.googleusercontent.com/b7O_l1-o7eakfDg9o9qJ9g00ye58yBzNdz8GpBPe1UNMFXRLBrKGG9-ISS6ySYixM_J4K_B0sjRMB35lMCY-L5o1xy35RKoNvkK9DJRZxJwKhfcBllvGTeb8ISutT3COkilDIzZf)

![](https://lh5.googleusercontent.com/Gs3Et4WOxDpXvX3GNbpi01kzrCJRt8dz3HUAsZo3biskWeX0y_wtOP6jf8zrWlcPt9pPIkWYOg4kPWg4qDIxgWK67p4wpyoblTGLe9pJWhlH9Ic1tVWuBc1f2gIwPiDx6NALnBwq)

Within this project, we will create an experiment that trains the model.

![](https://lh4.googleusercontent.com/sT36nm05vKwzHerzVFzIIcoZkNz-y276d92Ca4COxVa-XRlbugowz1nEVBNP4d3iiqRRXbfg5xOcDlaIGEpf-gemNsF5GfuPSJsPmhqACBUWqHrpXHP5HHrMiqGQsyEHgXL8S6t4)

Experiment Builder is a wizard-style GUI tool to submit a job to the Job Runner component.

The first step is to choose a machine type for scheduling the job. Gradient takes advantage of Google Compute Engine’s preempt**i**ble instances to provide low-cost infrastructure. Make sure you check the Enable low-cost instances checkbox. Choose G1 machine type that comes with 1 CPU core, 1.7GB RAM, and 250GB SDD. This configuration is sufficient for the Scikit-learn training job. For TensorFlow and PyTorch, you can select a GPU-based machine type for accelerating the job.

![](https://lh5.googleusercontent.com/ffAyjA9PSN3z-S7yeD5csih4FBhQAIXCzbkleqeeIRyXGKsTMzo2a3T93HUYp8YFN1XaiWK6puCcKJEMdioiDvbb-uiY16zcffyhV5wNKFxFs7WBSQ4i3IYXbVwdvQkWtC9jI5Ni)

In Gradient, jobs are based on a container image that provides the runtime and dependencies. For this tutorial, we are using an image that contains Python 3 runtime with Scikit-learn framework. I built the image by adding Python dependencies to the lightweight Alpine Linux image.  

![](https://lh5.googleusercontent.com/6n0Ef8BYBstWWKppitRAmKwmiZxI17IKxcRebunmuzUxGl9OQAGJNNthSXoJhvHyWiJoeTvzK_txk_tYo1Mj3XR_vL2hd8AGBuX2ZO_-c4UVXQ6JPtYjXDQKc1bkGKc_jzyMwdDD)

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

![](https://lh6.googleusercontent.com/HyhJ1-1p00POBKtsG4bl1axKcYQOCz880CRVrdDS9g82qb9-ptSyDYittaXOHstxraiWZd3YcNlqwUUgyAOuf3aTJY3birXJMjXYKusmeMIfQXIAvl29HXjuRHAVpm7omTr6Y82x)

Finally, let’s define the command for the job which is the Python script that executes within the context of the runtime of the container. When the script exits gracefully, the job is marked as complete.

The command for this job is `python train/train.py -i ./data/sal.csv -o /storage/salary`. The script, `train.py`, takes the source location of the dataset \(`sal.csv`\) and the target location to save the training model \(`/storage/salary)`.

In Gradient, any file that is saved at `/storage` location becomes available to other jobs and experiments. By persisting the model to this location, we will be able to access it from the inference job.

![](https://lh4.googleusercontent.com/uMi5VCHRM-bIpvMrM0lpFcVSbwTI4q3y1JdIk5w_l08hg0eKyHcaOvUlaCtIg9oTamIEgX7q3JW5dr3FeR6YW54Gd_JLM_0NDpHLVU_r7wBf-3P2xasZ6MTIuA9kAic4hsVbguEO)

We are now ready to kick off the training job by clicking on the Submit Experiment button.

Gradient adds the job to the queue and schedules it in one of the chosen machine types. In a few minutes, the job execution completes.

You can verify the logs that show the coefficients like Mean Square Error \(MSE\), Intercept, and Slope printed to the stdout in the code.

Feel free to explore the environment and files section of the job.

![](https://lh3.googleusercontent.com/XtstOTN1HDpTq-EODcD4g9iSypT70Vu_yhCTYAIdea0c4iKG0qZnC_XkjX1YAEPcH8XhmKbRryGMNIghn2m5VV3Vf8Z2f2sBYotL2j8SDosrZxiERcZGY_WylDJJUlR__GP13wLQ)

The fully trained and pickled model \(`model.pkl`\) is now available at `/storage/salary` location. You can now safely delete the job to clean up the project.

## **Hosting and Serving the Model**

With the training job done, we will now host a long-running job that exposes a REST endpoint for serving the model. The GitHub repo has the code for loading the pickled model file and running a Flask-based web server.

Start by creating a new job with the following parameters. Notice that it is similar to the training job except the command `pip install flask && python deploy/infer.py -m /storage/salary/model.pkl`.

We first install the Flask module and then launch `infer.py` which picks up the model file `/storage/salary/model.pkl`. Feel free to explore the code of `infer.py` to understand how I load the pickled model file and wire it to the GET request.

Since we are running a web server, we also need to enable port mapping. This is done by entering 8080:8080 in the Ports section of the job.

![](https://lh3.googleusercontent.com/w0SWsgKE2hQ7DlKZrKeSntlWssuVc-pz8E8mFyVxJhBll3fcmWnJrrMevU0py9PS2gtF78uRskM76G21vQvbdQuSHjBeX6uV1st_OlSdjtAflcQK2uKUrQfYEwUnvCBVgzCi5SZ0)

Submit the experiment and wait for the job to enter the running mode.

The logs from the job confirm that the web server is up and running.

![](https://lh5.googleusercontent.com/uBLUkUhS6jWYLI_UPHb5I2guMhaa4yiU9Do1VgdQ9bFBIIv3B8-xaIx51RrqSAeTuhGOLnBlV0tjSODiNkdKVoCKODjIlA01PLbFAK2x5ob7Jh6mUNS8cqlj3qVlBamGpBBrJUSp)

Before we can send a GET request to the endpoint, we need to access the URL of the job which is available under the Environment section.

![](https://lh3.googleusercontent.com/CX17z7EsfFN_q29WuZ_U0i9OZWd-jQtroixeBACAWgFeEDrwxnjjaRamvbmgnFmjZ-92uQqapA4cHFYLhglpW7wGlMMO-leYO26it9ICmTEDBg49vR0XiOtDzdUjwad0T93mm2Im)

Open a terminal window and invoke the REST endpoint.  
****

```bash
curl joyn52q2ns0g9.gradient.paperspace.com:8080/sal/25
```

The output below shows the predicted salary of a developer with 25 years of experience.

![](https://lh3.googleusercontent.com/5sA0kJRe0IK7Fk6qiffPuc-6lBH8Uv2JOljfIF_OV8I5xlGpOAPr-OEg9135evnwXYSMRzXaoy2LVO8Pwf5J-Cyg30Q1KknwbUQBVEOFfHtxqnjHs2IcxKeU2aLUINWN1Hk7VP66)

Gradient projects and experiments make it extremely simple to train and serve machine learning models. The same workflow can be initiated from the CLI which is good for automating the jobs.  


