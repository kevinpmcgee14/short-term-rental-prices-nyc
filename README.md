# Build an ML Pipeline for Short-Term Rental Prices in NYC


This project was completed as part of the [Udacity Machine Learning DevOps Engineer NanoDegree](#https://www.udacity.com/course/machine-learning-dev-ops-engineer-nanodegree--nd0821). And an initial project starter was forked from [here](#https://github.com/udacity/nd0821-c2-build-model-workflow-starter). The project prompt is as follows:

```
You are working for a property management company renting rooms and properties for short periods of 
time on various rental platforms. You need to estimate the typical price for a given property based 
on the price of similar properties. Your company receives new data in bulk every week. The model needs 
to be retrained with the same cadence, necessitating an end-to-end pipeline that can be reused.

In this project you will build such a pipeline.
```

## Project Results

* [GitHub Repo](#https://github.com/kevinpmcgee14/short-term-rental-prices-nyc)
* [W&B Project](#https://wandb.ai/kevin_mcgee/nyc_airbnb?workspace=user-kevin_mcgee)
* [W&B Final Run](#https://wandb.ai/kevin_mcgee/nyc_airbnb/runs/12dd8o1k?workspace=user-kevin_mcgee)
* [W&B Produciton Model Artifact](#https://wandb.ai/kevin_mcgee/nyc_airbnb/artifacts/model_export/random_forest_export/6e29e7f00a6cf4c29a05)

## Final Pipeline
![Final Pipeline](FinalPipeline.png?raw=true)

## Running the pipeline
In order to run the pipeline when you are developing, you need to be in the root of the starter kit, 
then you can execute as usual:

```bash
>  mlflow run .
```
This will run the entire pipeline.

When developing it is useful to be able to run one step at the time. Say you want to run only
the ``download`` step. The `main.py` is written so that the steps are defined at the top of the file, in the 
``_steps`` list, and can be selected by using the `steps` parameter on the command line:

```bash
> mlflow run . -P steps=download
```
If you want to run the ``download`` and the ``basic_cleaning`` steps, you can similarly do:
```bash
> mlflow run . -P steps=download,basic_cleaning
```
You can override any other parameter in the configuration file using the Hydra syntax, by
providing it as a ``hydra_options`` parameter. For example, say that we want to set the parameter
modeling -> random_forest -> n_estimators to 10 and etl->min_price to 50:

```bash
> mlflow run . \
  -P steps=download,basic_cleaning \
  -P hydra_options="modeling.random_forest.n_estimators=10 etl.min_price=50"
```
