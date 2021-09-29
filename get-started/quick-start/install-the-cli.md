---
description: How to install the Gradient Command Line Interface
---

# Install the Gradient CLI

This is an optional procedure for those who wish to interact with Gradient via the command line interface \(CLI\), in addition to the GUI or SDK.

## Installation

{% embed url="https://youtu.be/t1-PqoeqFuo" caption="Learn how to install the Gradient CLI. 1m35s." %}

The Gradient CLI is available on [PyPI](https://pypi.org/project/gradient/) and works on Windows, MacOS, and Linux.

The CLI requires **Python 3.4+** \(or Python 2.7\). Be sure to use a compatible version of **pip** \(or **pip3**\) depending on your Python version.

{% hint style="info" %}
**Pro Tip!** We highly recommend installing and using the CLI within a Python virtual environment. This will minimize conflicts with existing libraries on your computer. We recommend **virtualenv**. [See below](install-the-cli.md#using-a-virtual-environment) for more instructions.
{% endhint %}

## Install the CLI

#### **Using pip to install the latest stable release**

```bash
pip install -U gradient
```

The `-U` option upgrades all specified packages to the newest available version.

You can verify that it is working by running

```bash
gradient version
```

which will output a version like `v1.8.6`.

## Connecting your account

You can either stash your API key on your computer or include your API key on each command. The latter can be useful if you are working on several teams at the same time, as each team has its own API key.

### Set your active API key

First, [obtain an API Key](install-the-cli.md#obtaining-an-api-key), and then:

```bash
gradient apiKey XXXXXXXXXXXXXXXXXXX
```

Alternatively, you can set the environment variable `PAPERSPACE_API_KEY` temporarily to override your configured api key.

```bash
export PAPERSPACE_API_KEY=XXXX
gradient workflows run ...
```

**Note:** You can reveal your current API key with `cat ~/.paperspace/config.json`

## Obtaining an API key

{% embed url="https://www.youtube.com/watch?v=WS\_xYiaTSIY" caption="Obtain an API key from the settings page. 1m27s." %}

Sign in to your [Paperspace account](https://www.paperspace.com/account/login) and create a new API key. You'll use the API keys you generate here to authenticate your requests.

## Using a virtual environment

For Python 3.4+

First, install `virtualenv`:

```bash
pip install virtualenv
```

Create a new virtual environment:

```bash
python3 -m virtualenv <virtual_env_dir_path>
```

Activate the virtual environment:

```bash
source <virtual_env_dir_path>/bin/activate
```

Virtualenvs can also be run in other ways, e.g., using `conda`.

## Enable autocomplete

Add the following to your `.bashrc` \(or `.zshrc`\) to enable autocomplete anytime you activate your shell. If Gradient was installed in a virtual environment, the following has to be added to the `activate` script:

`eval "$(_GRADIENT_COMPLETE=source gradient)"`

Alternatively, you can create an activation script by:

`(_GRADIENT_COMPLETE=source gradient) > ~/paperspace_complete.sh`

and then add `. ~/paperspace_complete.sh` to your `.bashrc`, `.zshrc` or `activate` script.

For more, see [https://click.palletsprojects.com/en/7.x/bashcomplete/](https://click.palletsprojects.com/en/7.x/bashcomplete/) .

## **Install the latest pre-release version**

If you need a pre-release version of the CLI use the following command to install it:

```bash
pip install -U --pre gradient
```

