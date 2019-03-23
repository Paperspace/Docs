---
description: How to install the Paperspace CLI
---

# Install the CLI

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

## 

