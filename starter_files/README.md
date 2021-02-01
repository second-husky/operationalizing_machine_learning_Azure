# Machine Learning Pipeline Building using Azure AutoML

This project aimed to using machine learning to predict the potential customers for bank marketing based on the given data of potential customer's characteristics. 
It used Azure as a cloud platfrom to build an auto machine learning pipeline.

## Architectural Diagram

1) automated ML experiment: run an automated ML experiment to search for and optimized a best model
2) deploy the best model: deploy the best model for future consumption
3) enable logging: create the logging for the automated run 
4) swagger documentation: use swagger as a tool for easier documentation of how to consume the endpoints via http requests
5) consume model endpoints: consume the endpoint by sending http request to use the best model to make predictions based on new input data
6) create publish and consume a pipeline: a pipeline was created and published for future consumption of the endpoint


## Key Steps

First the bank marketing data was digested into a registered dataset named Bank-marketing
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_registered_datasets.PNG)

Then an autoML experiment was submitted to select the best model for deployment
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_completed_experiment.PNG)

After the experiment completed, the best model selected was shown below
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_the_best_model.PNG)

This best model was deployed. The application insights was enabled through sdk
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_endpoint_application_insights_enabled.PNG)

Logs was gotten by running the logs.py through command line
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_logs.PNG)

To make consuming endpoints easier, swagger was run on localhost showing the HTTP API methods and responses for the model
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_swagger_on_localhost.PNG)

Then interaction with the endpoint was realized by passing in JSON string inputs and JSON output was produced from the model. 
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_endpoint_json_output.PNG)

The endpoint was benchmarked using Apache bench
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_the_benchmarking.PNG)

Then a pipeline was created, published and consumed through sdk.

created pipeline
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_pipeline_created_and_run.PNG)

and the pipeline endpoint
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_pipeline_endpoint.PNG)

A REST endpoint has been created and remained active
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_active_rest_endpoint.PNG)

Run details were captured showing the step runs
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_run_details_steps_run.PNG)
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_run_details_pipeline.PNG)

The scheduled run is running
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_scheduled_run_in_ML_Studio.PNG)

## Screen Recording

screen cast
https://www.youtube.com/watch?v=c1PIT_MEDAc

## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.
The way to consume the endpoints can be made more user friendly by adding in data conversion to JSON format, so that input data is not limited to JSON
