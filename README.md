# Operationalizing Machine Learning  | Azure ML Studio

In this project, we are going through the all the processes that are needed to deploy our machine learning model on Azure for the end users. Though, this repository is useful to create Ml-Ops Pipeline for organisations.

## Architectural Diagram
![Architecture](./images/azure_pipeline.jpg)

*TODO*: Provide an architectual diagram of the project and give an introduction of each step. An architectural diagram is an image that helps visualize the flow of operations from start to finish. In this case, it has to be related to the completed project, with its various stages that are critical to the overall flow. For example, one stage for managing models could be "using Automated ML to determine the best model". 

## Key Steps
The key steps are as follows.
1. Model Configuration & Training
    
    To operationalize the ML model for end users, first we should have our prepared dataset and model configuration for that dataset should be ready which is **Bank marketing** dataset in our case.
    ![Dataset](./images/1-bank_marketing_dataset.PNG)
    
    After the model configuration, we have to start the experiment and wait for the experiment to get complete.
    
    After the successfuly run of the experiment, we would have the best model. In our case it is **Voting Classifier**.
    
    ![Successfull Run](./images/2-automl-complete.PNG)
    ![BestModel](./images/3-best-automl-model.PNG)
    
2. Deployment
    
    After getting the best model, now we are good to go for the deployment of the best model. We can deploy the model by clicking the **Deploy** button given in model details.
    
    When the deployment gets successfull, we can see our Rest API endpoint under the endpoints section of Azure ML Studio.
    
    ![Deployment](./images/4-bestmodel-deployed-endpoint.PNG)
    
3. Consume
    
    Completing the above deployment process, we have our endpoint ready to consume. But before that there are some checklist we need to follow to ensure the stability of the endpoint.
    
    To do that we have following checklist.
    - Enable Logs
      
      This step is need to check whether our enpoint gets successfulyy deployed or not.  
      ![EnableInsights](./images/5-enabled-insights-logs.PNG)
      
      After enabling the log, we will able to see the insight url in ML Studio.
      ![EnableInsights](./images/6-insight-url.PNG)
      
    - Make rest call to endpoint
      
      When we make an API call to our endpoint with sample data, we are able to see the inference output of the model.      
      ![ConsumeModelEndpoint](./images/8-endpoint-consumption.PNG)
      
    - Benchmark the endpoint
      
      However, just getting working enpoint is not enough, Thus, we also have measure the time taken by enpoint to give the output. By doing this, we can ensure that our endpoint's performance for end-user.
4. Swagger Documentation
    
    At this point, we have our model endpoint is ready and consummable but we also have to document the endpoint so that the other developers can able to understand the usecase of the endpoint.
    
    Swagger document can be available in endpoint details section as a *swagger.json* file.
    
    ![SwaggerDocumentation](./images/7-swagger-explore.PNG)
    
5. Pipeline Automation
    
    All the above steps, needs manual intervation for each thing. To automate above steps, Azure ML provides this pipeline option.
    
    In this pipeline, the developer have to create a python script or notebook with following steps.
    1. Create an Experiment in an existing Workspace.
    2. Create or Attach existing AmlCompute to a workspace.
    3. Define data loading in a TabularDataset.
    4. Configure AutoML using AutoMLConfig.
    5. Use AutoMLStep
    6. Train the model using AmlCompute
    7. Explore the results.
    8. Test the best fitted model.
    
    Through these above steps, we can also automate the MLOps pipeline through one script.
    
    Following are screenshout which we can see in Azure ML Studio.
    1. Pipeline Creation
    ![PipelineCreation](./images/10-pipeline-creation.PNG)

    2. Pipeline Runnning
    ![PipelineRunning](./images/11-pipeline-creation-running.PNG)

        ![PipelineRunning](./images/12-pipeline-experiment-running.PNG)
    
    3. Pipeline Complete
    ![PipelineComplete](./images/13-pipeline-run-complete.PNG)

    4. Pipeline Run Log
    ![PipelineRunLog](./images/14-pipeline-notebook-run-widget-log.PNG)

    5. Pipeline Endpoint Active
    ![PipelineEndPoint](./images/15-pipeline-endpoint-active.PNG)
    
    6. Pipeline End Point URL
    ![PipelineEndPointURL](./images/16-pipeline-endpoint-rest-url.PNG)
    
    7. Deallocate Compute Cluster
    ![RemoveComputeCluster](./images/17-compute-cluster-deletion.PNG)

## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:

## Standout Suggestions
- There should be a option to set enable push notification on failure/suceess of the deployment/training process.
- There should also have one option allowing the developer to choose type of documentation to download. Like swagger or postman.
- It would be nice if we can automate the pipeline for CNN type algorithms.
