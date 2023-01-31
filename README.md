# Mlflow-tracking-image
The project focused on tracking an experiment in tensorflow.

### About the project
MLflow tracking experiment is applied here for tracking the lifecyle and related aspects of tensorflow experiment. The epochwise updating of metrics are used to analyse the progress of working. All required parameters are recorded by logging necessary parameters into the api. Output of experiment is logged into artifacts, which helps to understand basic requirements for successful working of experiment.

## Getting Started
### Mlflow
MLflow is an open source platform to manage the end-to-end ML lifecycle. It hooks four main functions:MLflow tracking,MLflow projects,MLflow models and MLlfow registry.

#### Installation
MLflow can be installed using the command: 
**_pip install mlflow_**

#### Documentation
Official documentation for MLflow can be found at https://mlflow.org/docs/latest/index.html.

#### How to use MLflow
* **Initialization of experiment**    
After installing MLflow, now try to implement a basic machine learning pipeline and integrate MLflow into the workflow. 
1. Import all the packages we will need in our experience.
* **Setting up basic MLflow enviornment**   
2. New experiment with an experiment name can be created using mlflow.set_experiment("Experiment_name") method. If an experiment with same name already exists, the same will get ready for execution. Otherwise, it will go to create a new experiment.
3. Then, we can put new run name as mlflow.set_tag("mlflow.runName", "run_name"). Now the  new experiment will be created with the given details.
4. You can now use your MLcode to create an experiment.
5. The next, but important step is to setup a prerequirement for fetching each components of tensorflow model into mlflow api. After successful setting up of Ml model, we create a custom_callback. A callback is a powerful tool to customize the behavior of a Keras model during training, evaluation, or inference. All callbacks subclass the **keras.callbacks.Callback** class, and override a set of methods called at various stages of training, testing, and predicting. Callbacks are useful to get a view on internal states and statistics of the model during training.   
  class Classname(keras.callbacks.Callback):    
The description of creating callbacks are avilable in https://www.tensorflow.org/guide/keras/custom_callback.
6. Under the custom callback we define the logs.  Here uses the _epoch_level method(training only)_ as:   
  def on_epoch_end(self, epoch, logs=None):    
An epoch is when all the training data is used at once and is defined as the total number of iterations of all the training data in one cycle for training the machine learning model. The number of epochs is considered a hyperparameter. It defines the number of times the entire data set has to be worked through the learning algorithm.   
7. All the metrics that we want to track are put in a dict under the same class. Then the _on_epoch_end_ method records the metrics after each epoch ends and update them on mlflow run accordingly.

#### ML Workflow
MLflow supports all kind of Machine Learning experiments. The only difference is to keep track in our analysis/experiment. MLflow categorizes these into 3 main categories:   
* Parameters (via mlflow.log_param() )- Parameters are variables that you change or tweak when tuning your model. Here we uses the total number of epochs, image height, image width as parameters.
* Metrics (using mlflow.log_metric() )- Metrics are values that you want to measure as a result of tweaking your parameters. Typical metrics that are tracked can be items like F1 score, RMSE, MAE etc.
* Artifacts (using mlflow.log_artifact() )- Artifacts are any other items that you wish to store. Typical artifacts that we can keep track of are pickled models , PNGs of graphs, lists of feature importance variables.    

#### MLflow Tracking experiments
Tracking allows to create an extensive logging framework around the model. This component allows to log codes, custom metrics, data files, config and results. It also allows to query the experiments through which one can visualize and compare their experiments and parameters quickly without much struggle. 

The mlflow.search_runs() function helps to get all the details about our experiments or we can use autolog option to automatically track all the details of experiment. 8. The start_run is a manual method here we go with it.   
9. To get connection with already created experiment we use condition nested=True in start_run() method. Now new run will get into the already created experiment.   
Required parameters and model are logged into mlflow api using log_param and log_model.    
10. Artifact is the output of experiment. Here we uses the plot of Training v/s validation accuracy and training v/s validation loss.    
11. The artifact can be logged using log_artifact.

#### MLflow Tracking UI
12. We can navigate the Mlflow User Interface by typing http://127.0.0.1:5000 in a navigator , you will have access to a more detailed view,Start it with:
**_mlflow ui_**
13. After running the experiment the MLflow dashboard will display the given experiment_name, under this we get our runs.
14. The https://mlflow.org/docs/latest/tracking.html#logging-data-to-runs will help us to modify experiment as per requirements.
