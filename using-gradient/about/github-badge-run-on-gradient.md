# Run on Gradient \(GitHub badge\)

![Run on Gradient Badge attached to a GitHub repo](../../.gitbook/assets/screen-shot-2020-02-17-at-8.47.13-pm.png)





## What is it?

The Run on Gradient badge allows you to run a Gradient Notebook from any public GitHub repository on a free GPU. Gradient Notebooks are a hosted Jupyter notebook service from Paperspace that requires no setup and provides free access to computing resources including GPUs.

## How it Works

The "Run on Gradient" badge allows you to run a Gradient Notebook from any GitHub repository. Clicking the badge will take you to a static page where you can view the full contents of the notebook. From this page, you can either sign in or create an account to run the notebook for free. Making an account is completely free and can be done in a few clicks by signing up with Google, GitHub, or email. Then just select “Run Notebook on a Free GPU” and Gradient will spin up a free, fully interactive notebook instance.

![](../../.gitbook/assets/screen-shot-2020-08-19-at-9.47.39-am.png)

![](../../.gitbook/assets/screen-shot-2020-08-19-at-9.47.54-am.png)

## Using the "Run on Gradient" badge

Simply add the following code snippet to your `Readme.md` on your public GitHub repo:

```text
[![Gradient](https://assets.paperspace.io/img/gradient-badge.svg)](https://console.paperspace.com/github/huggingface/nlp/blob/master/notebooks/Overview.ipynb)
```

The HTML equivalent is:

```text
<a href="https://console.paperspace.com/github/huggingface/nlp/blob/master/notebooks/Overview.ipynb">
  <img src="https://assets.paperspace.io/img/gradient-badge.svg" alt="Run on Gradient"/>
</a>
```

Remember to replace the notebook URL in this template with the notebook you want to link to.

### **Notes**

**Workspace**: When you launch a new notebook from this button, Gradient will pull in the individual `.ipynb` file \(specified in the snippet above\) as a workspace. Optionally, if you would like to pull in the entire cloned GitHub repo as a workspace, append a `?clone=true` query parameter.  
  
**Runtime:** You can also optionally specify a Docker container to run this workspace in. You can point to any public container by appending `?runtime=paperspace/fastai` where you replace `paperspace/fastai` with your container name.  


## **FAQ**

### Does this work with private GitHub repos?

Currently, the 1-click "launch on gradient" button will only work with public GitHub repositories. If you would like to use a private GitHub repository or a container that is in a private registry, you can do so by clicking "Change instance type \(advanced\)" before running the notebook \(or alternatively, visiting the "Create Notebook" page in the Paperspace Console. 

### Where can I find the "Run on Gradient" Badge

The badge can be found here: [https://assets.paperspace.io/img/gradient-badge.svg](https://assets.paperspace.io/img/gradient-badge.svg) . 

It looks like this:

![Run on Gradient Badge](https://assets.paperspace.io/img/gradient-badge.svg)



