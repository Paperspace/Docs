---
description: How to install the Paperspace CLI
---

# Install the CLI

## Installation

The Paperspace CLI is available on [pypi](https://pypi.org/project/paperspace/) and [anaconda](https://anaconda.org/paperspace/paperspace) and works on Windows, MacOS, and Linux.

{% hint style="info" %}
**ProTip!** We recommend using installing and using CLI within a virtual environment. This will minimize any conflicts with existing libraries on your computer. 
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

![API keys section of the console \(https://www.paperspace.com/console/account/api\)](../.gitbook/assets/image%20%282%29.png)

