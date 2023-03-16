# Lesson 03: NLP Pipelines
## 01: NLP and Pipelines

### Natural Language Processing Pipelines
In this lesson, you'll be introduced to some of the steps involved in a NLP pipeline:

Text Processing
Cleaning
Normalization
Tokenization
Stop Word Removal
Part of Speech Tagging
Named Entity Recognition
Stemming and Lemmatization
Feature Extraction
Bag of Words
TF-IDF
Word Embeddings
Modeling

## 02: How NLP Pipelines Work
The 3 stages of an NLP pipeline are: Text Processing > Feature Extraction > Modeling.

- Text Processing: Take raw input text, clean it, normalize it, and convert it into a form that is suitable for feature extraction.
- Feature Extraction: Extract and produce feature representations that are appropriate for the type of NLP task you are trying to accomplish and the type of model you are planning to use.
- Modeling: Design a statistical or machine learning model, fit its parameters to training data, use an optimization procedure, and then use it to make predictions about unseen data.

This process isn't always linear and may require additional steps.

## Stage 1: Text Processing
The first chunk of this lesson will explore the steps involved in text processing, the first stage of the NLP pipeline.

- Extracting plain text: Textual data can come from a wide variety of sources: the web, PDFs, word documents, speech recognition systems, book scans, etc. Your goal is to extract plain text that is free of any source specific markup or constructs that are not relevant to your task.
- Reducing complexity: Some features of our language like capitalization, punctuation, and common words such as a, of, and the, often help provide structure, but don't add much meaning. Sometimes it's best to remove them if that helps reduce the complexity of the procedures you want to apply later.

### What Text Processing Will You Do in This Lesson?
You'll prepare text data from different sources with the following text processing steps:

1. Cleaning to remove irrelevant items, such as HTML tags
2. Normalizing by converting to all lowercase and removing punctuation
3. Splitting text into words or tokens
4. Removing words that are too common, also known as stop words
5. Identifying different parts of speech and named entities
6. Converting words into their dictionary forms, using stemming and lemmatization

After performing these steps, your text will capture the essence of what was being conveyed in a form that is easier to work with.

## Cleaning
Let's walk through an example of cleaning text data from a popular source - the web. You'll be introduced to helpful tools in working with this data, including the requests library, regular expressions, and Beautiful Soup.

[Notebook: Cleaning](https://github.com/chloehuang123/Udacity-Nano-Degree-Data-Scientist/blob/main/Lesson%2003:%20NLP%20Pipelines/cleaning_practice.ipynb)

[Notebook: Normalization](https://github.com/chloehuang123/Udacity-Nano-Degree-Data-Scientist/blob/main/Lesson%2003:%20NLP%20Pipelines/normalization_practice.ipynb)
