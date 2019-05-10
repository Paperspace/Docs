# Create a Model

### Example Use

Here is an example command for running an TensorFlow based experiment which generates a model summary, used in GradientCI, and also uploads model checkpoint files to permanent storage. 

`paperspace-python experiments createAndStart singlenode \  
--name Test1 \  
--workspaceUrl https://github.com/Paperspace/mnist-sample \  
--projectHandle <projectHandle> \   
--container tensorflow/tensorflow:1.13.1-py3 \  
--machineType K80 \  
--command 'python mnist.py \  
--data_format=channels_last' \  
--modelType Tensorflow --modelPath '/artifacts'`

