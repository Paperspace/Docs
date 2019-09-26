---
description: How to install the Gradient Command Line Interface
---

# Install the Gradient CLI

## Installation

{% embed url="https://youtu.be/t1-PqoeqFuo" caption="" %}

The Gradient CLI is available on [pypi](https://pypi.org/project/paperspace/) and works on Windows, MacOS, and Linux.

The CLI requires **Python 2.7** or **Python 3.4+**. Be sure to use a compatible version of **pip** depending on your Python version.

{% hint style="info" %}
**ProTip!** We recommend installing and using the CLI within a Python virtual environment. This will minimize conflicts with existing libraries on your computer. We recommend **virtualenv**.

**Python 2.7**  
Install virtualenv:

```bash
pip install virtualenv
```

Create new virtualenv:

```bash
virtualenv <env_directory_path>
```

Activate virtualenv:

```bash
source <env_directory_path>/bin/activate
```

**Python 3.4+**  
Create new virtualenv:

```bash
python3 -m venv /path/to/new/virtual/environment
```

Activate virtualenv:

```bash
source /path/to/new/virtual/environment/bin/activate
```
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

```bash
gradient apiKey XXXXXXXXXXXXXXXXXXX
```

#### Alternative: Include your API key for each command

```bash
gradient experiments run ... --apiKey XXXXXXXXXXXXXXXXXXX
```

## Obtaining an API key

First, sign in to your [Paperspace account](https://paperspace.com/). On the left of your home console, you should find an 'API' section. There, you'll find a form where you can create API keys. You'll use the API keys you generate here to authenticate your requests.

![API keys section of the console \(https://www.paperspace.com/console/account/api\)](../.gitbook/assets/image%20%289%29.png)

