# Plagiarism Detector - AWS SageMaker

This is the source code for a project which detects plagiarism between two sets of texts.

The project is hosted in an AWS SageMaker Jupyter Notebook. 

### Project Breakdown

There are 3 notebooks in this project. 
1. Data exploration, also called Exploratory Data Analysis (EDA)
2. Feature Engineering
3. Training the model

We also have our "train.py" file in source_sklearn, which contains the training sequence/model for our project. 

When we specify a custom training model in SageMaker, we need to specify an "entry point". 'train.py' file serves as the entry point for our model here.

### 
