# mlopszoomcamp-2024

For week2 we will learn experiment tracking with mlflow.
Create a new conda environment with python 3.9 and install the [requirements.txt](requirements.txt)
```            
conda activate mlflow-experimenttracking
```

Then run requirements.txt
```
pip install -r requirements.txt
```

Check installed requirements are present using
```
pip list
```

check mlflow using below. It sould show options for version and help.
```
mlflow
```
Run below to get mlflow version

```
mlflow --version
```
I got below mlflow, version 2.13.0

Run mlflow with below command.
```
mlflow ui --backend-store-uri sqlite:///mlflow.db
```
## MLFlow experiment tracking
Run the [script](./duration-prediction.ipynb) to understand how mlflow logging and experiment tracking (params, metrics etc) is done. 
Below set of lines start an experiment. 
```
import mlflow

mlflow.set_tracking_uri("sqlite:///mlflow.db")
mlflow.set_experiment("nyc-taxi-experiment")
```

All the information wrapper under the mflow start_run method can be tracked for various params and metrics as below

```
//anything under this method can be tracked
with mlflow.start_run():
    //set tagging to help with filtering
    mlflow.set_tag("developer", "amohan")
    //log params
    mlflow.log_param("train-data-path", "./data/

    alpha = 0.01
    //log params
    mlflow.log_param("alpha", alpha)

    mlflow.log_metric("rmse", rmse)
```
All values of this experiment can be viewed in mlflow ui.

Model can be logged in two ways.In option 1 less information is stored compared to option 2. You can use the option 2 way to retrieve the model and run it later as a python function, or docker container, cloud envs, etc.
```
mlflow.log_artifact("models/preprocessor.b", artifact_path="preprocessor")

or 

mlflow.xgboost.log_model(booster, artifact_path="models_mlflow")
```
