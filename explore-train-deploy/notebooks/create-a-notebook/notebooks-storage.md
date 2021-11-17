# Persistent Storage

## About

Every notebook in your account automatically includes a persistent filesystem. Use this directory to store datasets, model checkpoints, and more.  

![](../../../.gitbook/assets/image%20%2884%29.png)

### Notebook file structure

Your account will have a `/storage` directory automatically generated in your account at signup. When you create a notebook, a directory matching the notebook ID is created within the root `/storage` directory. When you upload data to a notebook, it will reside within this directory. As long as you don't delete your notebook, this data will be persisted.  If you need to share data across notebooks, just copy or move the data to the root `/storage` directory.  

### Storage size

This quota/size is determined by the team subscription so can range from 5GB up to 1TB. [Contact sales](https://info.paperspace.com/contact-sales-gradient) if you need to increase this limit beyond what is available with the default subscription plans. **Note:** Overage charges are incurred when users exceed the amount of data included in their subscription plan. Users who exceed that limit will be charged $0.29 for every additional GB used.

## Importing data

When uploading data, the files will be uploaded to a directory matching the ID of the notebook.  The root \(one level up\) is `/storage` where all your notebook data resides. 

### From your computer

Just click the upload icon to import data from your computer.  If there are a large number of files, it's advisable to zip them up first. **Note:** Your notebook must be running in order to import data. 

![](../../../.gitbook/assets/image%20%2879%29.png)

### Importing data from the web

Downloading data to `/storage` is as simple as using `curl` or `wget` from a Notebook [terminal](notebook-terminals.md) or Jupyter cell.  

## Exporting data

Downloading files is as simple as clicking the menu icon on a file \(the three vertical dots\) and clicking Download. **Note:** Your notebook must be running in order to download data. 

![](../../../.gitbook/assets/image%20%2877%29.png)



