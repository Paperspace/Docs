---
description: For inference/model serving
---

# Create a Deployment via the UI

## Create a Deployment

Deployments can be created through the web console. Deployments can be found under the `Deployments` tab of any Project. A list of all deployments across projects can be found in the `Deployments` tab on the sidebar. 

### Navigate to your trained models

![You can view your list of pretrained models at https://www.paperspace.com/console/models](../.gitbook/assets/screen-shot-2019-06-24-at-7.52.52-pm.png)

### Select the model & click deploy

![](../.gitbook/assets/screen-shot-2019-06-24-at-7.56.06-pm.png)

### Choose a machine type to run the deployment

![K80 machine has been selected for deployment](../.gitbook/assets/screen-shot-2019-06-24-at-8.00.25-pm.png)

The following block shows the region of the selected machine  & where the deployment will be served out of

![K80 in GCP West](../.gitbook/assets/screen-shot-2019-06-24-at-8.02.46-pm.png)

### Input Parameters for the deployment

**2. Name: Here we select a name of "Sample Deployment"** 

**3. Base Image: We use the tensorflow/serving:latest-gpu container, which is selected by default.** As both CPU & GPU serving is available, make sure to select the container corresponding to selected machine type & what your model was optimized for. Only tensorflow serving can be selected as base image \(support for any base image will be available for serving soon\).

![](../.gitbook/assets/screen-shot-2019-06-24-at-8.05.42-pm.png)

#### 4. Instance Count: Select the number of instances to run the deployment on. 

Here we chose 2, meaning there will be 2 K80 GPU instances backing this deployment. Load balancing is provided for all multi-instance deployments.

#### 5. Command to run at container launch

For the Tensorflow Serving base container used here, the command to run the job is unneeded. This becomes available to those choosing a different base image to deploy on.

![](../.gitbook/assets/screen-shot-2019-06-24-at-8.15.24-pm.png)

### Active Deployment vs Inactive Deployment

In the above example, we chose to create an active deployment \(selected by default\). You can also choose to create a deployment but not activate it. You are only charged for active deployments.

![](../.gitbook/assets/screen-shot-2019-06-24-at-8.17.48-pm.png)

### Deploying

Navigating to the deployments tab, you can see your list of active & inactive deployments. Here we have 3 deployments. 

![](../.gitbook/assets/screen-shot-2019-06-24-at-8.25.05-pm.png)

Each deployment has its own unique ID & is associated with the Experiment & Model it was created from. Clicking Start will launch the deployment

![](../.gitbook/assets/screen-shot-2019-06-24-at-8.37.24-pm.png)

Each deployment has its own unique endpoint which can be accessed via REST at https://services.paperspace.io/model-serving/\[your-model-id\]:predict

The number of running instances & the instance count are visible as well.



