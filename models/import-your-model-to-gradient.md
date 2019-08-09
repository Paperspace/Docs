# Import models to Gradient

Importing a model file trained elsewhere to be saved and then deployed within Gradient is very straight forward.

Just create an experiment that uploads or reads in the desired model file, specifying the  appropriate `--modelType` value, \(e.g. `Tensorflow`\)  and a `--modelPath` location \(example `"/artifacts"`\) within the experiment. The model will be automatically  parsed by Gradient and made available in your Model List for 1-click model deployment.

