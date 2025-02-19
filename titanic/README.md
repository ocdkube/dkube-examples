# Titanic example from Kaggle

# Notebook Details :

[owner project setup notebook](owner/resources.ipynb) - shows how to setup projects using DKube SDK. Skip the below project workflow steps, if you are creating the project and other resources by running this notebook. Jump to step 4 directly.

## Project Workflow:

### Step 1: Create Dkube code repo for titanic-owner:
1. Click on Repos in left pane and then click on +Code.
2. Name: titanic
3. Git URL: https://github.com/oneconvergence/dkube-examples.git
4. Branch: tensorflow

### Step 2 : Create a Project in DKube
1. Click on Projects in left pane in Dkube.
2. Click on + Create Project.
3. Give a project name, say titanic.
4. Check the enable leaderboard option and click on submit.
5. Click on titanic project and click on evaluation tab and then select the evaluation source repo as titanic created in step 1.
6. Give the evaluation script as `python titanic/owner/eval.py` and click on save button.

### Step 3 :Upload Train & Eval dataset: 
1. Click on Repos in left pane and then click on +dataset.
2. Details to be filled for train dataset:
   - Name: titanic-train
   - DataSource: Other 
   - URL: https://dkube.s3.amazonaws.com/datasets/titanic/train.csv
3. Details to be filled for test dataset
   - Name: titanic-test
   - DataSource: Other
   - URL: https://dkube.s3.amazonaws.com/datasets/titanic/test.csv

## Data Scientist Workflow:
The pipeline.ipynb file automatically creates a code repo named titanic-code, featuresets (titanic-train-fs and titanic-test-fs) for the user, and titanic-model using DKube SDK.

### Step 4 : Launch JupyterLab IDE in the project titanic
1. Click on IDEs in left pane and then select your titanic project from top.
2. Click on +JupyterLab and then fill the below details:
   - Give a name : titanic-{user}, replace {user} with your username.
   - Select code as titanic
   - Select Framework as tensorflow and version as 2.0.0 and then click on submit.
3. Open JupyterLab under the actions tab and go to workspace/titanic/titanic and then run all the cells of pipeline.ipynb file.
4. Preprocessing, Training and Predict runs will be automatically created in Dkube.

### Training Results
1. Go to your project titanic.
2. Navigate to the **leaderboard** to see the results that shows the accuracy and loss metrics.
3. Training metric results can be viewed from the runs tab in Dkube, with the tag as `dkube-pipeline` and type as `training`.

### Test Inference
1. Navigate to the model (titanic-model) and click on test inference.
2. Give the test inference name, say titanic.
3. The serving image is ocdr/tensorflowserver:2.0.0.
4. Check transformer option, and type the transformer script as titanic/transformer.py
5. Choose CPU, and submit.
6. Go to `https://<URL>:32222/inference`
   - Copy the model serving URL from the test inference tab.  
   - Copy the auth token from developer settings  
   - Select model type sk-stock  
   - Copy the contents of https://raw.githubusercontent.com/oneconvergence/dkube-examples/tensorflow/titanic/titanic_sample.csv and save then as CSV, and    upload.  
   - Click predict.

## Deploy Model (DKube version 2.1.x.x)
- Navigate to Repos-> Models-> titanic-model : select a model version
- Deploy
- Give name: titanic-deploy
- Transformer: click on transformer checkbox.
- Change the transformer script to: titanic/transformer.py.
- Submit

### Release, Publish and Deploy (Dkube version 2.2.x.x)

1. *Release Model*
- Click on model name titanic-model .
- Click on Release Action button for latest version of Model.
- Click on Release button and then the model will be released.

2. *Publish Model*
- Click on Publish Model icon under ACTIONS column.
- Give the publish model name.
- Select the serving image as ocdr/tensorflowserver:2.0.0
- Click on Transformer checkbox.
- Change transformer code to titanic/transformer.py.
- Click on Submit.

3. *Deploy Model*
- Click on Model catalog and select the published model.
- Click on the deploy model icon  under ACTIONS column.
- Enter the deploy model name and select CPU and click Submit.
- The state changes to deployed.
- Check in Model Serving and wait for the deployed model to change to running state.
- Deployed Model can used to test the prediction.

4. *Inference*
-  Go to `https://<URL>:32222/inference`
-  Go to model serving tab and copy the prediction endpoint of titanic-model and paste in model serving URL.
-  Copy the auth token from developer settings and paste in Authorization Token.  
-  Select model type as sk-stock  
-  Copy the contents of https://raw.githubusercontent.com/oneconvergence/dkube-examples/tensorflow/titanic/titanic_sample.csv and save then as CSV, and upload.  
-  Click predict.

