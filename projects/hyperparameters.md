# Hyperparameter Tuning

## About
Gradient provides users the ability to tune hyperparameters for their machine learning models, harnessing the power of our cloud to explore different model configurations and discover an optimal model.

## Initiating 
### For a GradientCI (GitHub-integrated) project
* In your `config.yaml` file, specify the domain of parameters over which Hyperopt should search.
* See GradientCI docs for information on how experiments will be triggered from code pushed to your GitHub repository.

### For a standalone projects
* CLI commands?

## Viewing hyperparameter search progress
* To see the progress of your hyperparameter search experiment, navigate to your GradientCI project in the Gradient
application. Select the hyperparameter search experiment and go to the "Hyperparameters" tab.
* You will see a visual display of all the jobs triggered by the experiment.

## Selecting the optimum model
* Once the hyperparameter search is finished, Gradient will automatically save the highest-performing model and
associate it as the model output of your experiment.
