# Registering Models in Gradient

## **Objectives**

* Understand the workflow involved in registering models
* Passing environment variables through Gradient CLI
* Persisting model files in Gradient Storage
* Registering Tensorflow Models in Gradient 

## **Introduction**

Experiments in Gradient can generate machine learning models, which can be interpreted and stored in your Project's Models list. This list holds references to the model and checkpoint files generated during the training period as well as summary metrics associated with the model's performance, such as accuracy and loss.

In this tutorial, we will create an experiment to generate a Keras model based on the [Fashion MNIST dataset](https://www.kaggle.com/zalando-research/fashionmnist). We will learn techniques such as passing environment variables to jobs, specifying the right container image, and mentioning the path to store the model artifacts.

The model is trained in Keras but it is finally exported as a TensorFlow model through `tf.saved_model.simple_save`method. This approach seralizes Keras session into a TensorFlow `.pb` file.

Start by cloning the repo [https://github.com/janakiramm/fashionmnist](https://github.com/janakiramm/fashionmnist) that contains the code for training and inferencing the model.

## Create a Project for Fashion MNIST

We will start by creating a project that can contain multiple experiments we may run during the training.

```text
gradient projects create --name Fashion
```

## Create an Experiment to Train the Model 

We will now start an experiment within the project created above. Make a note of the project id before proceeding further.

Switch to the train directory of the cloned Github repo.

```text
cd train
```

```text
gradient experiments run singlenode \
  --name fmnist \
  --projectId prioax2c4 \
  --experimentEnv "{\"EPOCHS\":5}" \
  --container tensorflow/tensorflow:1.9.0-gpu \
  --machineType K80 \
  --command "python train.py --modelPath /storage/model --version 1" \
  --modelType Tensorflow \
  --modelPath "/storage/model"
```

The above command has multiple switches that are important to the job. Let’s understand each of them.

The `singlenode` parameter runs the job on a single host.

`--name` assigns a friendly name to the experiment.

`--projectId` associates the experiment with an existing project.

`--experimentEnv` passes environment variables to the script. In our code, we decide the number of epochs based on the value defined in the EPOCHS environment variable.

`--container` parameter points the job to a container image used for the training job. Notice that we are passing an image that can advantage of a GPU-based machine.

`--machineType` schedules the job in one of the preferred instances. In our case, we are using K80 machine type that comes with an NVIDIA K80 GPU. Since the container and machine type are based on GPU, the job exploits the CUDA and cuDNN for accelerated training.

`--command` instructs the job to execute the script along with the passed parameters. The script expects the path to store the final model artifacts along with the version number. Since we are using a sub-directory under the `/storage` directory, the files stored are persisted across experiments. The model files stored here are used to register the TensorFlow model with Gradient. Feel free to explore [train.py](https://github.com/janakiramm/fashionmnist/blob/master/train/train.py) to understand how environment variables and command line parameters can be used to target Gradient specific features while keeping the code independent.

`--modelType` switch indicates that the job generates a valid TensorFlow model which can be managed by Gradient. Frameworks other than TensorFlow will be supported in the future.

`--modelPath` tells Gradient where to look for the model artifacts. This is typically `/artifacts` or `/storage` location. We are passing `/storage/model` directory which was used within the code.

Within a few seconds of running the command, you should see the logs displayed on the screen.

```text
Archiving your working directory for upload as your experiment workspace...(See https://docs.paperspace.com/gradient/experiments/run-experiments for more information.)
Removing existing archive
Creating zip archive: train.zip
100% (1 of 1) |########################################| Elapsed Time: 0:00:00 Time:  0:00:00

Finished creating archive: train.zip
Uploading zipped workspace to S3
100% (3108 of 3108) |##################################| Elapsed Time: 0:00:00 ETA:  00:00:00
100% (3108 of 3108) |##################################| Elapsed Time: 0:00:00 Time:  0:00:00
Uploading completed
New experiment created and started with ID: e720893n7f5vx
Awaiting logs...
js3v54dfgz1zcu	1	Downloading data from http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-labels-idx1-ubyte.gz
32768/29515 [=================================] - 0s 4us/step
40960/29515 [=========================================] - 0s 3us/step
js3v54dfgz1zcu	4	Downloading data from http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz
26427392/26421880 [==============================] - 2s 0us/step
26435584/26421880 [==============================] - 2s 0us/step
js3v54dfgz1zcu	7	Downloading data from http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz
16384/5148 [===============================================================================================] - 0s 0us/step
js3v54dfgz1zcu	9	Downloading data from http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-images-idx3-ubyte.gz
4423680/4422102 [==============================] - 1s 0us/step
4431872/4422102 [==============================] - 1s 0us/step
js3v54dfgz1zcu	12	2019-06-29 06:30:41.922354: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
js3v54dfgz1zcu	13	2019-06-29 06:30:42.014405: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:897] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
js3v54dfgz1zcu	14	2019-06-29 06:30:42.014841: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1392] Found device 0 with properties:
js3v54dfgz1zcu	15	name: Tesla K80 major: 3 minor: 7 memoryClockRate(GHz): 0.8235
js3v54dfgz1zcu	16	pciBusID: 0000:00:04.0
js3v54dfgz1zcu	17	totalMemory: 11.17GiB freeMemory: 11.09GiB
js3v54dfgz1zcu	18	2019-06-29 06:30:42.014881: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1471] Adding visible gpu devices: 0
js3v54dfgz1zcu	19	2019-06-29 06:30:42.345929: I tensorflow/core/common_runtime/gpu/gpu_device.cc:952] Device interconnect StreamExecutor with strength 1 edge matrix:
js3v54dfgz1zcu	20	2019-06-29 06:30:42.345995: I tensorflow/core/common_runtime/gpu/gpu_device.cc:958]      0
js3v54dfgz1zcu	21	2019-06-29 06:30:42.346006: I tensorflow/core/common_runtime/gpu/gpu_device.cc:971] 0:   N
js3v54dfgz1zcu	22	2019-06-29 06:30:42.346329: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1084] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 10748 MB memory) -> physical GPU (device: 0, name: Tesla K80, pci bus id: 0000:00:04.0, compute capability: 3.7)
js3v54dfgz1zcu	23	_________________________________________________________________
js3v54dfgz1zcu	24	Layer (type)                 Output Shape              Param #
js3v54dfgz1zcu	25	=================================================================
js3v54dfgz1zcu	26	Conv1 (Conv2D)               (None, 13, 13, 8)         80
js3v54dfgz1zcu	27	_________________________________________________________________
js3v54dfgz1zcu	28	flatten (Flatten)            (None, 1352)              0
js3v54dfgz1zcu	29	_________________________________________________________________
js3v54dfgz1zcu	30	Softmax (Dense)              (None, 10)                13530
js3v54dfgz1zcu	31	=================================================================
js3v54dfgz1zcu	32	Total params: 13,610
js3v54dfgz1zcu	33	Trainable params: 13,610
js3v54dfgz1zcu	34	Non-trainable params: 0
js3v54dfgz1zcu	35	_________________________________________________________________
js3v54dfgz1zcu	36	Epoch 1/5
58080/60000 [============================>.] - ETA: 0s - loss: 0.5437 - acc: 0.8103
60000/60000 [==============================] - 7s 112us/step - loss: 0.5406 - acc: 0.8113
js3v54dfgz1zcu	39	Epoch 2/5
60000/60000 [==============================] - 5s 82us/step - loss: 0.4034 - acc: 0.8597
js3v54dfgz1zcu	41	Epoch 3/5
57536/60000 [===========================>..] - ETA: 0s - loss: 0.3718 - acc: 0.8697
60000/60000 [==============================] - 5s 88us/step - loss: 0.3715 - acc: 0.8698.8698
js3v54dfgz1zcu	44	Epoch 4/5
54944/60000 [==========================>...] - ETA: 0s - loss: 0.3508 - acc: 0.8760
60000/60000 [==============================] - 6s 92us/step - loss: 0.3514 - acc: 0.876059
js3v54dfgz1zcu	47	Epoch 5/5
59488/60000 [============================>.] - ETA: 0s - loss: 0.3391 - acc: 0.8794
60000/60000 [==============================] - 5s 85us/step - loss: 0.3392 - acc: 0.8795.8794
10000/10000 [==============================] - 0s 45us/step
js3v54dfgz1zcu	51
js3v54dfgz1zcu	52	Model accuracy: 0.8657
js3v54dfgz1zcu	53
js3v54dfgz1zcu	54	Model saved to /storage/model
js3v54dfgz1zcu	55
js3v54dfgz1zcu	56	PSEOF
```

## Verifying the Creation of Model

We can check if the output of the job is registered as a valid TensorFlow model with the following command.

```text
gradient models list
```

`+------+-----------------+------------+------------+----------------+   
| Name | ID | Model Type | Project ID | Experiment ID |   
+------+-----------------+------------+------------+----------------+   
| None | mosdnkkv1o1xuem | Tensorflow | prioax2c4 | e720893n7f5vx |   
+------+-----------------+------------+------------+----------------+`

The project id `(prioax2c4)` and experiment id `(e720893n7f5vx)` confirm that it is the model associated with the latest experiment.

You can also visit the Models section of Gradient UI to see a list of registered models.

![](../.gitbook/assets/grad-model-0.jpg)

## Summary 

After registering the model, we can turn that into a deployment to perform inferencing.

