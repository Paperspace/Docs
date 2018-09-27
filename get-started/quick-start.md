# Quick Start

## Prerequisites 

1. [Create a Paperspace account ](https://www.paperspace.com/account/signup)
2. [Install the Paperspace CLI ](quick-start.md#installation)
3. [Connecting your account](quick-start.md#connecting-your-account)

## Installation

The Paperspace CLI is available on [pypi](https://pypi.org/project/paperspace/) and [anaconda](https://anaconda.org/paperspace/paperspace) and works on Windows, MacOS, and Linux.

### Option 1: Using **pip** or **conda**

#### **Using pip**

```text
$ pip install paperspace
```

#### **Using conda**

```text
$ conda install -c paperspace paperspace
```

### Option 2: Download the binaries

Pre-built [binaries](https://github.com/Paperspace/paperspace-node#option-1-download-the-pre-built-paperspace-binary-for-your-plaftorm) are available for Windows, Mac, and Linux. These binaries enable you to run the CLI without any additional packages. Be sure to add the directory where the binary is installed to your path.

## Connecting your account

You can either log in via the command line or use your API key to connect your account.

### Login

```text
$ paperspace login
Email: myname@example.com
Password: ******
```

### Obtaining an API key

First, sign in to your [Paperspace account](https://paperspace.com/). On the left of your home console, you should find an 'API' section. There, you'll find a form where you can create API keys. You'll use the API keys you generate here to authenticate your requests.

![API keys section of the console \(https://www.paperspace.com/console/account/api\)](https://support.paperspace.com/hc/article_attachments/360002146454/gradient_api_request.png)

## Submit a job

You are now ready to run a job \(even without any code!\). You can run:

```text
$ paperspace jobs create --container Test-Container --command "nvidia-smi"
```

Your job will get uploaded to our cluster of machines. Behind the scenes, we are zipping the current working directory, creating a Docker container, and running the command you provided.

There are several optional Job parameters.  See the full list [here](../jobs/create-a-job.md#job-parameters).

{% hint style="info" %}
**Note:** the zipped upload of your working directory is limited to 100MB
{% endhint %}

## Monitor your Job progress

Job states go from **Queued** &gt; **Pending** &gt; **Running**

Once the Job is in a **Running** state, you can watch your Job run in the CLI and web UI. For example, you should see the output of `nvidia-smi` by running `paperspace jobs logs --tail`. 

A Job can complete with the following states: **Success**, **Cancelled**, or **Error**.

 Congratulations! You ran your first job on Gradient 🚀

Jobs have a ton of functionality that this quick example doesn't cover.  To learn more, view the [Jobs section](../jobs/create-a-job.md).

