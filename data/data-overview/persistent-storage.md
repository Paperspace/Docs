# Persistent Storage

## Persistent Storage

Persistent Storage is accessible across your Gradient Notebooks.  Uploading and downloading data is possible from any of these endpoints. 

## Importing data

When uploading data, the files will be uploaded to a directory matching the ID of the notebook.  The root \(one level up\) is `/storage` where all your notebook data resides. 

### From your computer

Just click the upload icon to import data from your computer.  If there are a large number of files, it's advisable to zip them up first. **Note:** Your notebook must be running in order to import data. 

![](../../.gitbook/assets/image%20%2879%29.png)

### Importing data from the web

Downloading data to `/storage` is as simple as using `curl` or `wget` from a Notebook [terminal](../../explore-train-deploy/notebooks/create-a-notebook/notebook-terminals.md) or Jupyter cell.  

## Exporting data

Downloading files is as simple as clicking the menu icon on a file \(the three vertical dots\) and clicking Download. **Note:** Your notebook must be running in order to download data. 

![](../../.gitbook/assets/image%20%2877%29.png)

