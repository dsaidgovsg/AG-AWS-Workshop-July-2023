# SageMaker Autopilot
## Creating an Autopilot Experiment

* SageMaker Autopilot automatically creates feature engineering pipelines, selects algorithms suitable for the machine learning problem type, trains and tunes several candidate models, before arriving at an optimal model.
* Steps carried out by Autopilot are as follows:
  * Automatic data pre-processing and feature engineering
    * Automatically handles missing data.
    * Provides statistical insights about columns in your dataset.
    * Automatically extracts information from non-numeric columns, such as date and time information from timestamps.
    * Automatically handles imbalance in data.
    * Automatically creates 10 feature engineering (FE) pipelines most adapted to your problem. Those FE pipelines consist of FE transformations coming from both native scikit-learn, and custom scikit-learn-compatible FE transformations invented and open-sourced by Amazon.
  * Automatic ML model selection
    * Automatically infers the type of predictions that best suit your data, such as binary classification, multi-class classification, or regression
    * Explores high-performing algorithms such as gradient boosting decision tree, feed-forward deep neural networks, and logistic regression, and trains and optimizes hundreds of models based on these algorithms to find the model that best fits your data.
    * Automatically cross validates the data to flag problems like over-fitting or selection bias and gives insights on how the model will generalize to an independent dataset.
  * Automatic Model HPO
    * Runs epsilon-greedy bandit tests for each of the FE pipelines, and progressively invests more HPO budget on the most rewarding FE pipeline.
  * Model leader-board
    * Automatically ranks the candidate models based on user provided success metric such as accuracy, precision, recall, or area under the curve (AUC).
    * Lets user automatically deploy the model for real-time inference that is best suited to their use case.
  * Explainability
    * Automatic notebook generation showcasing the various candidates (pipelines) for feature engineering.
    * Automatic notebook generation for exploratory data analysis.
    * Uses SageMaker Clarify under the covers to provide model agnostic feature attribution metrics using SHAPley values.
  * Automatic data and model provenance
    * Uses SageMaker Experiments behind the scenes to automatically capture data and model lineage for each of the candidate models trained during the process.

## Autopilot
* For the Autopilot experiment, we will be using a pre-transformed dataset which is similar to the result of the transformed features exported via Data Wrangler to S3. To Launch Autopilot on SageMaker Studio, click on File -> New -> Experiment. On the Create experiment page, fill in the details as shown below.
S3 location `s3://ag-aws-workshop-july23-dev/diabetic-readmission.csv`
![](./../img/3_low_code_0.png)
On the 'Target and Features' page, select Target Column as 'readmitted'.
![](./../img/3_low_code_7.png)
On the 'Training method and algorithms' page leave the default 'auto' setting.
On the 'deployment and advanced settings' page, select Access from the menu on the left and specify 'IAM role' as `arn:aws:iam::820788409827:role/ag-dev-studio-workshop-ExecutionRole`. This role provides permissions for Sagemaker Studio to work with AWS on our behalf.
![](./../img/3_low_code_8.png)
* Once the Autopilot experiment starts, you will see it complete stages one by one starting with the pre-processing stage as shown below.
![](./../img/3_low_code_5.png)
* Once the candidate definitions (i.e., 10 feature engineering pipelines) are generated, you will see 2 buttons that are enabled on the right upper corner of the workspace. Clicking those buttons take you to generated notebooks showing the code for feature engineering and data exploration.
![](./../img/3_low_code_3.png)
* Once all the stages are completed, you can see ranked list of all the trained models by Autopilot along with the captured metrics.
![](./../img/3_low_code_2.png)
* You can dive into the details of individual models by right clicking on the model and choosing Open in model details.
![](./../img/3_low_code_1.png)