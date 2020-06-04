---
description: How to install the Gradient Command Line Interface
---

# Install the Gradient CLI

## Installation

{% embed url="https://youtu.be/t1-PqoeqFuo" caption="" %}

The Gradient CLI is available on [pypi](https://pypi.org/project/gradient/) and works on Windows, MacOS, and Linux.

The CLI requires **Python 3.4+ \(**or **Python 2.7\)**. Be sure to use a compatible version of **pip** \(or **pip3**\) depending on your Python version.

{% hint style="info" %}
**Pro Tip!** We highly recommend installing and using the CLI within a Python virtual environment. This will minimize conflicts with existing libraries on your computer. We recommend **virtualenv**. [See below](install-the-cli.md#using-a-virtual-environment) for more instructions.
{% endhint %}

## Install the CLI

#### **Using pip to install the latest stable release**

```bash
pip install -U gradient
```

**Using pip to install the latest prerelease**

```bash
pip install -U --pre gradient
```

## Connecting your account

You can either stash your API key on your computer or include your API key on each command.

### Set your active API key

First, [obtain an API Key](install-the-cli.md#obtaining-an-api-key), and then:

```bash
gradient apiKey XXXXXXXXXXXXXXXXXXX
```

Alternatively, you can include your API key with each command:

```bash
gradient experiments run ... --apiKey XXXXXXXXXXXXXXXXXXX
```

**Note:** You can reveal your current API key with `cat ~/.paperspace/config.json`

## Obtaining an API key

{% embed url="https://www.youtube.com/watch?v=WS\_xYiaTSIY" %}

First, sign in to your [Paperspace account](https://www.paperspace.com/account/login). On the left of your home console, you will find an 'API' section. There, you'll find a form where you can create API keys. You'll use the API keys you generate here to authenticate your requests.

![API keys section of the console \(https://www.paperspace.com/console/account/api\)](../.gitbook/assets/image%20%2831%29.png)

## Enable autocomplete

Add following to your `.bashrc` \(or `.zshrc`\) to enable autocomplete anytime you activate your shell. If gradient was installed in a virtual environment, the following has to be added to the `activate` script:

`eval "$(_GRADIENT_COMPLETE=source gradient)"`

Alternatively, you can create activation script by:

`(_GRADIENT_COMPLETE=source gradient) > ~/paperspace_complete.sh`

and then add `. ~/paperspace_complete.sh` to your `.bashrc`, `.zshrc` or `activate` script.

More: [https://click.palletsprojects.com/en/7.x/bashcomplete/](https://click.palletsprojects.com/en/7.x/bashcomplete/)

## Using a virtual environment

First, install virtualenv:

```bash
pip install virtualenv
```

Python 3.4+

Create new virtual environment:

```bash
python3 -m virtualenv <virtual_env_dir_path>
```

Activate virtual environment:

```bash
source <virtual_env_dir_path>/bin/activate
```

Python 2.7 \(note that Python 2.7 will be deprecated in 2020\)  
Create new virtual environment:

```bash
virtualenv <virtual_env_dir_path>
```

Activate virtual environment:

```bash
source <virtual_env_dir_path>/bin/activate
```

