# Plagiarism Detector - AWS SageMaker

This is the source code for a project which detects plagiarism between two sets of texts.

The project is hosted in an AWS SageMaker Jupyter Notebook. We can also deploy the same model using AWS Lambda, create a model endpoint, and use the endpoint in a custom WebApp and provide our model as a service, just like a popular plagiarism detector service, [TurnItIn](https://www.turnitin.com/) . Since I have already created a web app for [movie review classification project](https://github.com/mohammadjafri1992/SentimentAnalysisWebApp), this step seems redundant here. Check out the model deployment using Flask [here](https://github.com/mohammadjafri1992/SentimentAnalysisWebApp)

### Project Breakdown

There are 3 notebooks in this project. 
1. Data exploration, also called Exploratory Data Analysis (EDA)
2. Feature Engineering
3. Training the model

We also have our "train.py" file in source_sklearn, which contains the training sequence/model for our project. 

When we specify a custom training model in SageMaker, we need to specify an "entry point". 'train.py' file serves as the entry point for our model here.


### Modeling approach

My modeling approach was very simple. After I performed exploratory data analysis (EDA) and got an overall veiw of the data, I performed feature enginering on the data corpus.

There are several apporachces to model this problem but I used the following two.
1. n-gram
2. Longest Common Subsequence (LCS)

You can read more about these approaches in [this paper](https://s3.amazonaws.com/video.udacity-data.com/topher/2019/January/5c412841_developing-a-corpus-of-plagiarised-short-answers/developing-a-corpus-of-plagiarised-short-answers.pdf).

In the my experimentation and implementation in the [2nd notebook](https://github.com/mohammadjafri1992/Plagiarism_detector_AWS_SageMaker/blob/master/2_Plagiarism_Feature_Engineering.ipynb), the N-gram approach seemed a bit "rigid" and we had to specify the length of 'n' and perform the operation in a fixed manner. The length of 'n' in N-gram varies on the context of the text. e.g. there may be much more common words in scientific papers because of the use of standardized and typical words, and their use in a specific context. Here, we may need to tune the value of 'n' for our n-gram comparison to a higher value.
If we have a set of general news articles, in which the "story" is the same, we should set 'n' to be very low as even the smallest similarity between the two texts can hint towards plagiarism.

The second approach, Longest Common Subsequence (LCS), seems very flexible and scalable as it generalizes the text comparison to almost any type/category/genre of text. This approach works well in my project as well.

Please look at the [2nd notebook](https://github.com/mohammadjafri1992/Plagiarism_detector_AWS_SageMaker/blob/master/2_Plagiarism_Feature_Engineering.ipynb) to make things even more clear. I have detailed explanation of the executed code cells there.


### SKLearn classifier vs. PyTorchModel using ANN

I used a simple SKLearn RandomForestClassifier against the PyTorchModel using ANN because of the limited amount of data I had. 

Deep Neural Networks work the best when we have a LOT of data because then the network gets enough "time" to first converge, then generalize itself. There is a very nice graph on page 24 of [Hands-on machine learning with Scikitlearn, Keras and Tensorflow by Aurelien Geron](https://www.amazon.com/Hands-Machine-Learning-Scikit-Learn-TensorFlow/dp/1492032646/ref=sr_1_1?crid=2PHFRLTVNUYA1&keywords=hands+on+machine+learning+with+scikit-learn+and+tensorflow+2&qid=1576451440&sprefix=hands+on+mac%2Caps%2C129&sr=8-1) which show that using more data clearly improves the model performance.

When we have smaller datasets, using classical machine learning models work the best, hence my selection of RandomForestClassifier.

In simple binary classification problems, it has been my experience in the past that we should start form any tree based models to get the best performance from the get-go, because they tend to work the best. 

You can read more about each code cell execution and its explanation in the [3rd notebook](https://github.com/mohammadjafri1992/Plagiarism_detector_AWS_SageMaker/blob/master/3_Training_a_Model.ipynb).








