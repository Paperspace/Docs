---
description: How to install the Paperspace CLI
---

# Install the CLI

## Installation

The Paperspace CLI is available on [pypi](https://pypi.org/project/paperspace/) and [anaconda](https://anaconda.org/paperspace/paperspace) and works on Windows, MacOS, and Linux.

{% hint style="info" %}
**ProTip!** We recommend installing and using the CLI within a Python virtual environment. This will minimize conflicts with existing libraries on your computer.

**Python 2.7 - 3.2**  
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

**Python 3.3+**  
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

#### **Using pip**

```bash
pip install paperspace
```

#### **Using conda**

```bash
conda install -c paperspace paperspace
```

## Connecting your account

You can either stash your API key on your computer or include your API key on each command.

### Set your active API key

```bash
paperspace-python apiKey XXXXXXXXXXXXXXXXXXX
```

#### Alternative: Include your API key for each command

```bash
paperspace-python experiments createAndStart ... --apiKey XXXXXXXXXXXXXXXXXXX
```

## Obtaining an API key

First, sign in to your [Paperspace account](https://paperspace.com/). On the left of your home console, you should find an 'API' section. There, you'll find a form where you can create API keys. You'll use the API keys you generate here to authenticate your requests.

![API keys section of the console \(https://www.paperspace.com/console/account/api\)](../.gitbook/assets/image%20%285%29.png)

