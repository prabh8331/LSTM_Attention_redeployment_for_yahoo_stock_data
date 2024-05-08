[![Build Status](https://dev.azure.com/jjuzaszek/LSTM_Attention_redeployment_for_yahoo_stock_data/_apis/build/status%2FJuliuszB12.LSTM_Attention_redeployment_for_yahoo_stock?branchName=main)](https://dev.azure.com/jjuzaszek/LSTM_Attention_redeployment_for_yahoo_stock_data/_build/latest?definitionId=19&branchName=main)

## High-level architecture overview
![architecture](https://github.com/JuliuszB12/LSTM_Attention_redeployment_for_yahoo_stock/assets/68758875/faf9f779-cde1-4bd1-9873-3ade8bf929aa)

## Description
Airbyte with yahoo source connector is sending data to Kafka topic at 1-minute intervals about 1-minute prices and volumes of chosen stocks.
At the same time Airflow DAG consuming that data and storing it in Azure blob storage. Every 15 minutes different Airflow DAG fetches updated blob storage data to retrain LSTM Attention machine learning model for predicting next 1-minute stock close price based on previous time-series of prices and calculated technical indicators and log it as a next run of experiment to MLflow model registry. After that new version of model is compared with model assigned with production alias on new validation data to either retain previous version of model as production version or change alias in MLflow and deploy new version of model to Azure ML Studio real-time inference endpoint hosted on Azure Kubernetes cluster. Described operations are executed within peered private networks and all privileges to access different resources are result of system-assigned managed identities of resources from which the code is executed without explicit mentioning of any connection secrets. Predictions of hosted model can be fetched from endpoint through Azure Function behind Azure API Management. Deployment of both containers and infrastructure is managed by Azure DevOps CI/CD pipelines within azure-pipelines.yaml file.

Development tech stack: TensorFlow/Keras, Kafka Python Client, Azure Python Client, Terraform, Azure Resource Manager template, Custom Script Extension, Docker Compose, azure-pipelines.yaml

## Step-by-step deployment
--desciption
