---
description: This guide explains how to use the terminal in Gradient Notebooks
---

# Terminal

## Introduction to notebook terminal

Terminals are useful for interacting with the underlying OS environment to perform a variety of tasks such as installing packages, organizing files, and more.&#x20;

![The terminal is available on Pro and Growth plan subscriptions in Gradient.](<../../.gitbook/assets/terminal command.gif>)

The terminal has root access in the notebook, which can be useful for a variety of tasks.

## How to gain terminal access in Gradient Notebooks

The terminal is currently available to Pro and Growth plan subscribers. [Gradient Pricing](https://gradient.run/pricing) provides a more detailed description of what else is available on upgraded plans, including superior free instance types and availability, additional storage, and more.

To open a terminal, use the **Terminal** icon in the sidebar. The notebook must be in the **Running** state.

![The Terminal button on the left sidebar provides terminal access.](../../.gitbook/assets/terminal-notebook-button.png)

To create a new terminal instance, use the `+` button in the left sidebar.

![Use the the + button in the terminal to create a new terminal window.](<../../.gitbook/assets/new terminal window.gif>)

There is no limit on the number of terminal windows that may run simultaneously.

## How to use bash in the terminal

Some users report that using bash in the terminal improves their work and reduces unexpected errors.

To use bash, enter the following command in the default shell:

```
bash
```

![To use bash in the terminal enter the bash command in the default terminal shell.](../../.gitbook/assets/bash.gif)

The terminal is now using bash.

## How to SSH into a notebook from a local terminal

{% hint style="warning" %}
WARNING: This is an experimental feature, please use at your own risk.
{% endhint %}

Steps to access a Gradient Notebook remotely using VSCode&#x20;

1. Start a notebook in the console. Right-click the jupyter icon and copy the URL (e.g.`https://nuv5vbc7ck.clg07azjl.paperspacegradient.com/?token=d4e87987b69a4480038673d1368e07e2`
2. Open VSCode
3. Type `cmd`+`shift`+`p` to open the Command Pallette
4. Choose `Jupyter specify local or remote....`
5. Paste in the URL
6. Open an `.ipynb` in VSCode. You will see the connection up top.

