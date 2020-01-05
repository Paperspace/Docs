# Train a Model with the CLI

### Objectives

**Prerequisites:**

* [Install Gradient CLI](https://github.com/dkobran/Docs/blob/master/get-started/install-the-cli.md)
* [Obtain an API Key](https://github.com/dkobran/Docs/blob/master/get-started/install-the-cli.md#connecting-your-account)

**Steps**

* Learn the workflow involved in training a model
* Use custom containers with experiments
* Create an experiment that trains a Scikit-learn model
* Share files and models across experiments

The experiment generates a Python pickle file that gets stored in the shared storage service of Gradient. 

### Creating a Gradient Experiment to Train the Model

In this step, we will generate a fully-trained model by submitting the dataset and Python code to Gradient. The output from this experiment is stored in a centrally accessible storage location that will be used in the next step of this tutorial.

Let’s take a minute to get familiar with the dataset. To keep this really simple, we are using one feature \(x\) that represents the years of experience of a candidate and a label \(y\) associated with the salary.

[![](https://camo.githubusercontent.com/59b528eaff4f097e23b67ee0c6237cdda1048f09/68747470733a2f2f6c68342e676f6f676c6575736572636f6e74656e742e636f6d2f3369745565445841557236736b6f57447445687457466e6c466c785a65786b45684d2d7239756b35346e3261775a6b6663616d5a74725f4941394e43425059413879513963667438552d4179486a4d41536972306b366430652d726b64482d6f4a4174754a49596b777a6f2d486869666c6374666d30674f5a4e4576505646414e6c4f44672d6965)](https://camo.githubusercontent.com/59b528eaff4f097e23b67ee0c6237cdda1048f09/68747470733a2f2f6c68342e676f6f676c6575736572636f6e74656e742e636f6d2f3369745565445841557236736b6f57447445687457466e6c466c785a65786b45684d2d7239756b35346e3261775a6b6663616d5a74725f4941394e43425059413879513963667438552d4179486a4d41536972306b366430652d726b64482d6f4a4174754a49596b777a6f2d486869666c6374666d30674f5a4e4576505646414e6c4f44672d6965)

The dataset, _sal.csv_, is available in the _data_ folder of the [GitHub](https://github.com/janakiramm/Salary) repo. Clone the repo to your local machine and open it in your favorite text editor to explore the data.

In the _train_ directory, you’ll find _train.py_, which is responsible for generating the model by applying linear regression to the dataset.

```python
import numpy as np
import pandas as pd
import os
from argparse import ArgumentParser
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

parser = ArgumentParser()
parser.add_argument("-i", "--in", dest="input",
                    help="location of input dataset")
parser.add_argument("-o", "--out",dest="output",
                    help="location of model"
                    )

dataset = parser.parse_args().input
model_dir = parser.parse_args().output

sal = pd.read_csv(dataset,header=0, index_col=None)
X = sal[['x']]
y = sal['y']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=10)

lm = LinearRegression() 
lm.fit(X_train,y_train) 

print('Intercept :', round(lm.intercept_,2))
print('Slope :', round(lm.coef_[0],2))

from sklearn.metrics import mean_squared_error
y_predict= lm.predict(X_test)
mse = mean_squared_error(y_predict,y_test)
print('MSE :', round(mse,2))

from sklearn.externals import joblib

if not os.path.exists(model_dir):
    os.makedirs(model_dir)
filename = model_dir+'/model.pkl'

joblib.dump(lm, filename)
```

Apart from applying linear regression, the code prints parameters such as intercept, slope, and MSE to stdout. The trained model is stored in the directory named _salary_ under `/storage` as a _.pkl_ file.

We are ready to kick off the training experiment on Gradient 🚀 Run the below command to submit the experiment.

The location `/storage` maps to Gradient persistent storage location. Anything stored at this location will be available even after the experiment is terminated. By storing the _.pkl_ file at `/storage`, we will be able to access it from the model serving experiment that exposes the REST endpoint.

```text
gradient experiments run singlenode \
--name train \
--projectId prj0ztwij \
--container janakiramm/python:3 \
--machineType C2 \
--command 'python train/train.py -i ./data/sal.csv -o /storage/salary' \
--workspaceUrl https://github.com/janakiramm/Salary
```

This command does quite a bit of heavy lifting for us. It schedules the training experiment in one of the chosen machine types and kicks off the training process.

Let’s analyze the steps taken by Gradient to finish the experiment.

1. The CLI downloads all the files \(including the dataset\) and uploads it to Gradient
   1. You can also run the experiment from your local system by not specifying the `--workspaceUrl` parameter! This compress all the files into a .zip file and upload it to Gradient.
2. Gradient pulls the container image instructed in the CLI \(`--container janakiramm/python:3`\) from the registry, which is Docker Hub for this scenario
3. Before running the container, Gradient maps the directory with the uploaded files to the container’s working directory
4. Gradient maps the command sent via the CLI parameter \(`--command 'python train/train.py -i ./data/sal.csv -o /storage/salary'`\) to the docker run command
5. Gradient schedules the container in one of the machines that match the type mentioned in the CLI \(`--machineType C2`\)

Once the experiment's status moves into run mode, it simply executes the code in the Python file. In _train.py_ that we uploaded, we do two things - print the coefficients like intercept, slope, MSE and copy the model into the `/storage` location.

The output from CLI confirms that the experiment has been successfully executed. If you navigate to the experiment in the UI, you will see the logs printed the coefficients used in the script along with the message `PSEOF` which is a healthy sign.

We are using a custom Docker container image with prerequisites such as NumPy, Scipy, Pandas, and Scikit-learn. This image was built from the official Python 3 Docker image.

