# Train & Deploy an ML Model with the Gradient CLI

## Objectives

* Install and configure the Paperspace CLI
* Learn the workflow involved in training a model
* Use custom containers with experiments
* Create an experiment that trains a Scikit-learn model
* Share files and models across experiments
* Create a long-running job \(web service\) that serves the model
* Access the REST endpoint exposed by a job

There are two Gradient experiments involved in this workflow--training and deployment. The first experiment generates a Python pickle file that gets stored in the shared storage service of Gradient. The same pickle file will be used by the second experiment running a Flask web server to expose a REST endpoint. This experiment will serve the model through the inferencing endpoint.

## Installing and Configuring the Paperspace CLI

To install the Gradient CLI, you'll first need to sign up for a [Paperspace account](https://www.paperspace.com/account/signup).

Once you’ve created your account, install the Gradient CLI.

{% hint style="info" %}
**ProTip!** We recommend installing and using the CLI within a Python virtual environment. This will minimize conflicts with existing libraries on your computer. We recommend **virtualenv**.
{% endhint %}

### **Creating a virtual environment \(optional\)**

Creating a directory _\*\*_for my virtual environment:

```bash
mkdir gradient
```

Create new virtual environment:

```bash
virtualenv gradient
```

Activate my new virtual environment:

```bash
source gradient/bin/activate
```

### **Install the CLI**

```bash
pip install -U gradient
```

Once you’ve created a Paperspace account and installed the CLI, you’ll next need to obtain an API key. Your API key will allow you to access the Gradient features from the command line. Each API key has an API Token name associated with it.

## Obtaining an API key  <a id="obtaining-an-api-key"></a>

First, sign in to your [Paperspace account](https://paperspace.com/). On the left of your home console, you should find an 'API' section. There, you'll find a form where you can create API keys. You'll use the API keys you generate here to authenticate your requests. API keys section of the console:

![API keys section of the console \(https://www.paperspace.com/console/account/api\)](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LHZRFUkajubOAmgu6Rd%2F-LdfHAvW1SCTEgQCIMBL%2F-LdfHBpYjeIWaedlGyv4%2Fimage.png?alt=media&token=2213be47-bdb4-4cee-a592-b8cc904eb01c)

### Set your active API key  <a id="set-your-active-api-key"></a>

```text
paperspace-python apiKey XXXXXXXXXXXXXXXXXXX
```

## Creating a Gradient Experiment to Train the Model

In this step, we will generate a fully-trained model by submitting the dataset and Python code to Gradient. The output from this experiment is stored in a centrally accessible storage location that will be used in the next step of this tutorial.

Let’s take a minute to get familiar with the dataset. To keep this really simple, we are using one feature \(x\) that represents the years of experience of a candidate and a label \(y\) associated with the salary.

![](https://lh4.googleusercontent.com/3itUeDXAUr6skoWDtEhtWFnlFlxZexkEhM-r9uk54n2awZkfcamZtr_IA9NCBPYA8yQ9cft8U-AyHjMASir0k6d0e-rkdH-oJAtuJIYkwzo-Hhiflctfm0gOZNEvPVFANlODg-ie)

The dataset, _sal.csv_, is available in the _data_ folder of the [GitHub](https://github.com/janakiramm/Salary) repo. Clone the repo to your local machien and open it in your favorite text editor to explore the data.

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

```bash
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

The output from Paperspace CLI confirms that the experiment has been successfully executed. If you navigate to the experiment in the UI, you will see the logs printed the coefficients used in the script along with the message `PSEOF` which is a healthy sign.

We are using a custom Docker container image with prerequisites such as NumPy, Scipy, Pandas, and Scikit-learn. This image was built from the official Python 3 Docker image.

## Creating a Gradient Experiment to Deploy and Host the Model

We are now ready to host the trained model in a Gradient experiment that runs a Flask web server. The experiment loads the pickle file created and stored by the last experiment at the `/storage` location.

Navigate to the deploy directory of the cloned repo to find _infer.py_.

```python
from flask import Flask, jsonify
from sklearn.externals import joblib
from argparse import ArgumentParser

parser = ArgumentParser()
parser.add_argument("-m", "--model", dest="model",
                    help="location of the pickle file")

filename = parser.parse_args().model

app = Flask(__name__)

@app.route('/')
def index():
    return "Stackoverflow Salary Predictor"

@app.route('/sal/<int:x>', methods=['GET'])
def predict(x):
    loaded_model=joblib.load(filename)
    y=loaded_model.predict([[x]])[0]
    sal=jsonify({'salary': round(y,2)})
    return sal

if __name__ == '__main__':
      app.run(host='0.0.0.0', port=8080)
```

This is a standard Flask web server listening on port 8080. It exposes `/sal` endpoint which takes the number of years of experience and returns the predicted salary.

Each time a request is made, it loads the latest version of the pickle file, calls the predict method, serializes the output in JSON and returns the response.

Since Flask is not a part of the container image used in the tutorial, we will need to install it with pip before running the script, which can be included in the run command.

To access the REST endpoint, we also need to instruct Gradient to map the container port to the host port. This is done through the CLI parameter `--ports`_._

Unlike the previous experiment, this wouldn’t get terminated unless it is manually stopped or destroyed. The Flask web server turns the experiment into a long-running experiment that doesn’t exit automatically.

Let’s go ahead and submit the experiment to Gradient.

```text
gradient jobs create \
--container janakiramm/python:3 \
--machineType C2 \
--ports 8080:8080 \
--command 'pip install flask && python deploy/infer.py -m /storage/salary/model.pkl'
```

The logs shown by the CLI confirms that the web server is up and running. Before we can access the endpoint, we need to get the DNS name of the experiment.

Hit _Ctrl+C_ to get back to the command prompt. Don’t worry! this doesn’t terminate the experiment but only exits the CLI.

Let’s explore the experiment details with the below command:

```bash
gradient jobs list
```

Make a note of the _fqdn_ parameter mentioned in the output. We need that to access the REST endpoint. Since we are using the _jq_ utility, we can also grab the _fqdn_ with a simple command.

$ export GRAD\_HOST=\`paperspace jobs list \| jq -r .\[\].fqdn\`

It’s time for us to hit the REST endpoint to get the predictions. Let’s check the expected salary of a candidate with 25 years of experience.

$ curl $GRAD\_HOST:8080/sal/25

{"salary":149121.27}

Congratulations! You have successfully completed the end-to-end workflow involved in training and deploying machine learning models with Gradient.

Let’s do the clean up by stopping and destroying the experiment.

```bash
export JOB_ID=`gradient jobs list | jq .[].id`
gradient jobs stop $JOB_ID
gradient jobs destroy $JOB_ID
```

## Summary

Gradient is an ML PaaS that removes the friction involved in configuring pipelines for data science and machine learning. Similar to a PaaS, developers, and data scientists can upload data and code to Gradient to train sophisticated models. The scalable infrastructure of Gradient can be used for model serving.

Apart from CLI, users can submit experiment through the web UI available within Paperspace Console. For interactive development, Jupyter Notebooks can be launched.

