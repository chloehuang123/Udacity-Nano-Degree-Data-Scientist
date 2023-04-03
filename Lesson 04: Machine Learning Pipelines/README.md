# Lesson 04: Machine Learning Pipelines

## Introduction
Welcome to this lesson on ML Pipelines! Here, we'll cover:

Advantages of Machine Learning Pipelines
Scikit-learn Pipeline
Scikit-learn Feature Union
Pipelines and Grid Search
Case Study

## Corporate Messaging Case Study
This corporate message data is from one of the free datasets provided on the [Figure Eight Platform](https://appen.com/pre-labeled-datasets/), licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

Next, you'll use NLP to process text data, much like what you'll be doing in the project.

[Case Study: Clean and Tokenize](https://github.com/chloehuang123/Udacity-Nano-Degree-Data-Scientist/blob/main/Lesson%2004:%20Machine%20Learning%20Pipelines/clean_tokenize.ipynb)

[Case Study: Machine Learning Workflow](https://github.com/chloehuang123/Udacity-Nano-Degree-Data-Scientist/blob/main/Lesson%2004:%20Machine%20Learning%20Pipelines/ml_workflow.ipynb)

## Using Pipeline
Below, you'll find a simple example of a machine learning workflow where we generate features from text data using count vectorizer and tf-idf transformer, and then fit it to a random forest classifier. Before we get into using pipelines, let's first use this example to go over some scikit-learn terminology.

- ESTIMATOR: An estimator is any object that learns from data, whether it's a classification, regression, or clustering algorithm, or a transformer that extracts or filters useful features from raw data. Since estimators learn from data, they each must have a fit method that takes a dataset. In the example below, the CountVectorizer, TfidfTransformer, and RandomForestClassifier are all estimators, and each have a fit method.
- TRANSFORMER: A transformer is a specific type of estimator that has a fit method to learn from training data, and then a transform method to apply a transformation model to new data. These transformations can include cleaning, reducing, expanding, or generating features. In the example below, CountVectorizer and TfidfTransformer are transformers.
- PREDICTOR: A predictor is a specific type of estimator that has a predict method to predict on test data based on a supervised learning algorithm, and has a fit method to train the model on training data. The final estimator, RandomForestClassifier, in the example below is a predictor.
In machine learning tasks, it's pretty common to have a very specific sequence of transformers to fit to data before applying a final estimator, such as this classifier. And normally, we'd have to initialize all the estimators, fit and transform the training data for each of the transformers, and then fit to the final estimator. Next, we'd have to call transform for each transformer again to the test data, and finally call predict on the final estimator.

### Without pipeline:
```
    vect = CountVectorizer()
    tfidf = TfidfTransformer()
    clf = RandomForestClassifier()

    # train classifier
    X_train_counts = vect.fit_transform(X_train)
    X_train_tfidf = tfidf.fit_transform(X_train_counts)
    clf.fit(X_train_tfidf, y_train)

    # predict on test data
    X_test_counts = vect.transform(X_test)
    X_test_tfidf = tfidf.transform(X_test_counts)
    y_pred = clf.predict(X_test_tfidf)
```    
Fortunately, you can actually automate all of this fitting, transforming, and predicting, by chaining these estimators together into a single estimator object. That single estimator would be scikit-learn's Pipeline. To create this pipeline, we just need a list of (key, value) pairs, where the key is a string containing what you want to name the step, and the value is the estimator object.

### Using pipeline:
```
pipeline = Pipeline([
    ('vect', CountVectorizer()),
    ('tfidf', TfidfTransformer()),
    ('clf', RandomForestClassifier()),
])

# train classifier
pipeline.fit(Xtrain)

# evaluate all steps on test set
predicted = pipeline.predict(Xtest)
```
Now, by fitting our pipeline to the training data, we're accomplishing exactly what we would by fitting and transforming each of these steps to our training data one by one. Similarly, when we call predict on our pipeline to our test data, we're accomplishing what we would by calling transform on each of our transformer objects to our test data and then calling predict on our final estimator. Not only does this make our code much shorter and simpler, it has other great advantages, which we'll cover in the next video.

Note that every step of this pipeline has to be a transformer, except for the last step, which can be of an estimator type. Pipeline takes on all the methods of whatever the last estimator in its sequence is. For example, here, since the final estimator of our pipeline is a classifier, the pipeline object can be used as a classifier, taking on the fit and predict methods of its last step. Alternatively, if the last estimator was a transformer, then pipeline would be a transformer.

## Advantages of Using Pipeline Part 1:
### 1. Simplicity and Convencience
- Automates repetitive steps - Chaining all of your steps into one estimator allows you to fit and predict on all steps of your sequence automatically with one call. It handles smaller steps for you, so you can focus on implementing higher level changes swiftly and efficiently.
- Easily understandable workflow - Not only does this make your code more concise, it also makes your workflow much easier to understand and modify. Without Pipeline, your model can easily turn into messy spaghetti code from all the adjustments and experimentation required to improve your model.
- Reduces mental workload - Because Pipeline automates the intermediate actions required to execute each step, it reduces the mental burden of having to keep track of all your data transformations. Using Pipeline may require some extra work at the beginning of your modeling process, but it prevents a lot of headaches later on.

## Advantages of Using Pipeline Part 2:
### 2. Optimizing Entire Workflow
- GRID SEARCH: Method that automates the process of testing different hyper parameters to optimize a model.
- By running grid search on your pipeline, you're able to optimize your entire workflow, including data transformation and modeling steps. This accounts for any interactions among the steps that may affect the final metrics.
- Without grid search, tuning these parameters can be painfully slow, incomplete, and messy.

### 3. Preventing Data leakage
- Using Pipeline, all transformations for data preparation and feature extractions occur within each fold of the cross validation process.
- This prevents common mistakes where you’d allow your training process to be influenced by your test data - for example, if you used the entire training dataset to normalize or extract features from your data.
- You'll see what we mean by this in a video later in this lesson about using Pipeline with GridSearchCV.

[Case Study: Build Pipeline](https://github.com/chloehuang123/Udacity-Nano-Degree-Data-Scientist/blob/main/Lesson%2004:%20Machine%20Learning%20Pipelines/pipeline.ipynb)

## Pipelines and Feature Unions
FEATURE UNION: Feature union is a class in scikit-learn’s Pipeline module that allows us to perform steps in parallel and take the union of their results for the next step.

A pipeline performs a list of steps in a linear sequence, while a feature union performs a list of steps in parallel and then combines their results.
In more complex workflows, multiple feature unions are often used within pipelines, and multiple pipelines are used within feature unions.

## Using Feature Union
Taking the example from the previous video, let's say you wanted to extract two different kinds of features from the same text column - tfidf values, and the length of the text. Your first approach might be to create an additional column from the text column called text_length like this. Then both text and text_length can be part of your feature matrix. But now your pipeline would break. You can't run CountVectorizer on NumPy arrays of strings and integers.
```
df['txt_length'] = df['text'].apply(len)
X = df[['text', 'txt_length']].values
y = df['label'].values
X_train, X_test, y_train, y_test = train_test_split(X, y)

pipeline = Pipeline([
    ('vect', CountVectorizer()),
    ('tfidf', TfidfTransformer()),
    ('clf', RandomForestClassifier()),
])

# train classifier
pipeline.fit(Xtrain)

# predict on test data
predicted = pipeline.predict(Xtest)
```
Let's say you had a custom transformer called TextLengthExtractor. Now, you could leave X_train as just the original text column, if you could figure out how to add the text length extractor to your pipeline. If only you could fit it on the original text data, rather than the output of the previous transformer. But you need both the outputs of TfidfTransformer and TextLengthExtractor to feed into the classifier as input.
```
X = df['text'].values
y = df['label'].values
X_train, X_test, y_train, y_test = train_test_split(X, y)

pipeline = Pipeline([
    ('vect', CountVectorizer()),
    ('tfidf', TfidfTransformer()),
    ('txt_length', TextLengthExtractor()),
    ('clf', RandomForestClassifier()),
])

# train classifier
pipeline.fit(Xtrain)

# predict on test data
predicted = pipeline.predict(Xtest)
```
- Feature unions are super helpful for handling these situations, where we need to run two steps in parallel on the same data and combine their results to pass into the next step.
- Like pipelines, feature unions are built using a list of (key, value) pairs, where the key is the string that you want to name a step, and the value is the estimator object. Also like pipelines, feature unions combine a list of estimators to become a single estimator. However, a feature union runs its estimators in parallel, rather than in a sequence as a pipeline does. In this example, the estimators run in parallel are nlp_pipeline and text_length. Notice we use a pipeline in this feature union to make sure the count vectorizer and tfidf transformer steps are still running in sequence.
```
X = df['text'].values
y = df['label'].values
X_train, X_test, y_train, y_test = train_test_split(X, y)

pipeline = Pipeline([
    ('features', FeatureUnion([

        ('nlp_pipeline', Pipeline([
            ('vect', CountVectorizer()
            ('tfidf', TfidfTransformer())
        ])),

        ('txt_len', TextLengthExtractor())
    ])),

    ('clf', RandomForestClassifier())
])

# train classifier
pipeline.fit(Xtrain)

# predict on test data
predicted = pipeline.predict(Xtest)
```
- Now, our pipeline doesn't break and uses both features! This would be equivalent to this code.
```
vect = CountVectorizer()
tfidf = TfidfTransformer()
txt_len = TextLengthExtractor()
clf = RandomForestClassifier()

# train classifier
X_train_counts = vect.fit_transform(X_train)
X_train_tfidf = tfidf.fit_transform(X_train_counts)

X_train_len = txt_len.fit_transform(X_train)
X_train_features = hstack([X_train_tfidf, X_train_len])
clf.fit(X_train_features, y_train)

# predict on test data
X_test_counts = vect.transform(X_test)
X_test_tfidf = tfidf.transform(X_test_counts)

X_test_len = txt_len.transform(X_test)
X_test_features = hstack([X_test_tfidf, X_test_len])
y_pred = clf.predict(X_test_features)
```
The tfidf transformer and the text length extractor are fit to the input data, in this case the raw data, independently. They are then performed in parallel, and their outputs are combined and passed to the next estimator, in this case, the classifier.

[Case Study: Add Feature Union](https://github.com/chloehuang123/Udacity-Nano-Degree-Data-Scientist/blob/main/Lesson%2004:%20Machine%20Learning%20Pipelines/feature_union_practice.ipynb)

## Creating Custom Transformer
In the last section, you used a custom transformer that extracted whether each text started with a verb. You can implement a custom transformer yourself by extending the base class in Scikit-Learn. Let's take a look at a a very simple example that multiplies the input data by ten.
```
import numpy as np
from sklearn.base import BaseEstimator, TransformerMixin

class TenMultiplier(BaseEstimator, TransformerMixin):
    def __init__(self):
        pass

    def fit(self, X, y=None):
        return self

    def transform(self, X):
        return X * 10
```
Remember, all estimators have a fit method, and since this is a transformer, it also has a transform method.

FIT METHOD: This takes in a 2d array X for the feature data and a 1d array y for the target labels. Inside the fit method, we simply return self. This allows us to chain methods together, since the result on calling fit on the transformer is still the transformer object. This method is required to be compatible with scikit-learn.
TRANSFORM METHOD: The transform function is where we include the code that well, transforms the data. In this case, we return the data in X multiplied by 10. This transform method also takes a 2d array X.
Let's test our new transformer, by entering the code below in the interactive python interpreter in the terminal, ipython. We can also do this in Jupyter notebook.
```
multiplier = TenMultiplier()

X = np.array([6, 3, 7, 4, 7])
multiplier.transform(X)
```
This outputs the following:
```
array([60, 30, 70, 40, 70])
```
Nice! Next, we'll create a custom transformer that has a bit more significance. Let's build a case normalizer, which simply converts all text to lowercase. We aren't setting anything in our init method, so we can actually remove that. We can leave our fit method as is, and focus on the transform method. We can lowercase all the values in X by applying a lambda function that calls lower on each value. We'll have to wrap this in a pandas Series to be able to use this apply function.
```
import numpy as np
import pandas as pd
from sklearn.base import BaseEstimator, TransformerMixin

class CaseNormalizer(BaseEstimator, TransformerMixin):
    def fit(self, X, y=None):
        return self

    def transform(self, X):
        return pd.Series(X).apply(lambda x: x.lower()).values

case_normalizer = CaseNormalizer()

X = np.array(['Implementing', 'a', 'Custom', 'Transformer', 'from', 'SCIKIT-LEARN'])
case_normalizer.transform(X)
```
Entering the code above in ipython outputs the following:
```
array(['implementing', 'a', 'custom', 'transformer', 'from',
       'scikit-learn'], dtype=object)

```
Awesome! It's a good idea to learn how to write your own custom functions - it allows you to have more control and flexibility with your machine learning pipelines.

Another way to create custom transformers is by using this FunctionTransformer from scikit-learn's preprocessing module. This allows you to wrap an existing function to become a transformer. This provides less flexibility, but is much simpler. You can learn more about this in the link below.

[Case Study: Create Custom Transformer]()
