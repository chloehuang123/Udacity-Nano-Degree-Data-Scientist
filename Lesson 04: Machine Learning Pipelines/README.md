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
