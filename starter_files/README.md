# Machine Learning Pipeline Building using Azure AutoML

This project aimed to using machine learning to predict the potential customers for bank marketing based on the given data of potential customer's characteristics. 
It used Azure as a cloud platfrom to build an auto machine learning pipeline.

## Architectural Diagram

 1） Upload data and create dataset in Azure ML studio
 
 2） Create and configure an AutoML step run an automated ML experiment in order to search for and optimized a best model
 
 3） Create and configure a pipeline with the AutoML step as the main step
 
 4） Run the pipeline and register the best model
 
 5） Deploy the best model and consume the endpoint
 
     Enable logging: create the logging for the endpoint consumption
     
     Swagger documentation: use swagger as a tool for easier documentation of how to consume the endpoints via http requests
     
     Consume model endpoints: test the endpoint by sending http request to use the best model to make predictions based on new input data
     
 6） Publish the pipeline: the pipeline was published to the workspace and a REST point was created to rerun the pipeline from any HTTP library on any platform


## Key Steps

### Data Digestion
The bank marketing data was uploaded from a csv file using a url link. After a cleaning step, the cleaned data was digested into a registered dataset named Bank-marketing as shown in the following screen shot and ready to be used in the AutoML training 
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_registered_datasets.PNG)

### AutoML Experiment Creation
An autoML experiment was configured and submitted to select the best model for deployment
Since this is a classification problem, the task was set to "classification".
Early stopping was enabled and auto featurization is also enabled in the AutoML run
Below screenshot shows the submited AutoML run with run ID and Status shows one run has completed successfully. Running time was 22m 10s and the compute target used was 'compute-for-auto'
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_completed_experiment.PNG)

After the experiment completed, the best model was selected. The best model used Voting Ensemble and achieved an accuracy of 0.91958 as shown in the below screenshot 
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_the_best_model.PNG)

The achieved AUC weighted is 0.9448 and the model contains XGboostclassifier as a step of the voting ensemble algorithm

### Model Deployment

This best model was registered and deployed as a web service. Below screenshots shows the endpoint that can be used to consume the model through REST API. The deployed model ID and the url of the REST endpoint are displayed. Both the authentication and the application insights were enabled. Application insights can be accessed through the bottom URL. The swagger.json file used to define the input data format can also be downloaded from the shown Swagger URL
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_endpoint_application_insights_enabled.PNG)

Log of the endpoint consumption was retrieved to monitor the process by running the logs.py through command line. The log shows the record of getting swagger.json file
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_logs.PNG)

### Model Consumption
To make consuming endpoints easier, swagger was run on localhost showing the HTTP API methods and responses for the model. Consumers can find the format of the input data from the post section.
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_swagger_on_localhost.PNG)

Then interaction with the endpoint was realized by passing in JSON string inputs and JSON output was produced from the model. The result in the following screenshot shows the prediction results that neither the two data entries are identified as target customer of the bank. Retrieving prediction data from the deployed best model through the endpoint is successful. 
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_endpoint_json_output.PNG)

Then The endpoint was benchmarked using Apache bench
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_the_benchmarking.PNG)

### Pipeline Publication
Since the autoML step and the model deployment has been tested, a pipeline was then created, published and consumed through sdk to enable automation.

A pipeline run named "Run 1" was created and currently running indicated by the status on this Pipelines page. It is associated with the pipeline-rest-endpoint experiment 
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_pipeline_created_and_run.PNG)

A pipeline endpoint named "Bankmarketing Train"is also created and the status shows it is active and ready to used to access the pipeline
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_pipeline_endpoint.PNG)
 
 The endpoint page also shows a REST endpoint has been created and remained active
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_active_rest_endpoint.PNG)

Run details were captured showing the step runs. The record from run details shows one run is being submitted
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_run_details_steps_run.PNG)
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_run_details_pipeline.PNG)

In the pipeline-rest-endpoint experiment page, the status of run 1 shows it is running with 1 step shown in the graph tab, which indicates the pipeline is running successfully as expected
![alt text](https://github.com/second-husky/operationalizing_machine_learning_Azure/blob/master/starter_files/screen-shots/screenshot_of_scheduled_run_in_ML_Studio.PNG)

## Screen Recording

screen cast
https://www.youtube.com/watch?v=c1PIT_MEDAc

## Possible Improvement:

The way to consume the endpoints can be made more user friendly by adding in data conversion to JSON format, so that input data is not limited to JSON
