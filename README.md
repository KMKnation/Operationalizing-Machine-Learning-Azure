# Operationalizing Machine Learning  | Azure ML Studio

In this project, We are going to demonstrate all the things required to make the best ML model live for end-user.

We will go through creating AutoML experiment to deploying model for end user.
Also we will evaluate the endpoint by consuming it.
We will check the stability and performance of the endpoint by enabling the logs and benchmarking the endpoint.
To allow other developers to understand the endpoint, we will demonstrate how to use swagger for it.

At last, to automate this process for dev-ops purpose, we will create one pipeline which uses the Azure SDK to perform all the above operations through [notebook](./aml-pipelines-with-automated-machine-learning-step.ipynb).

## Architectural Diagram
![Architecture](./images/azure_pipeline.jpg)

## Key Steps
The key steps are as follows.
1. Automated ML Experiment
    
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

[![Demo video](https://i.ytimg.com/vi/pndxfhW3kp0/0.jpg)](https://youtu.be/tzUU06RSUuk)

URL: [https://youtu.be/pndxfhW3kp0](https://youtu.be/tzUU06RSUuk)

## Future Improvement Suggestions
- Right now, we have to set the minimum cluster and maximum hours to train. But If we connect this both things just ask user to enter minutes to complete the whole automl cycle and the studio automatically allocates clusters to achieve concurrency would be great. However this is one of costlier thing to do but in some emergency scenario, it might be usefull one.
- Right now, this whole solution is on cloud. Hence, For first run, we are just experimenting which code gets run perfectly on cloud and keeps improving the pipeline which leads to multiple consumption of compute clusters or instances for just experiment. If in future there would be option to run the azure solution by using local computer's resource for experiments and then deploying the soluiton with azure cloud would be must cost savier.

## Standout Suggestions
- There should be a option to set enable push notification on failure/suceess of the deployment/training process.
- There should also have one option allowing the developer to choose type of documentation to download. Like swagger or postman.
- It would be nice if we can automate the pipeline for CNN type algorithms.
