### **The CRISP-DM Process (Cross Industry Process for Data Mining)**

The lessons leading up to the first project are about helping you go through CRISP-DM in practice from start to finish. Even when we get into the weeds of coding, try to take a step back and realize what part of the process you are in, and assure that you remember the question you are trying answer and what a solution to that question looks like.

`1.` Business Understanding

`2.` Data Understanding

`3.` Prepare Data

`4.` Data Modeling

`5.` Evaluate the Results

`6.` Deploy

The first two steps of CRISP-DM are:

1. Business Understanding - this means understanding the problem and questions you are interested in tackling in the context of whatever domain you're working in. Examples include

How do we acquire new customers?
Does a new treatment perform better than an existing treatment?
How can improve communication?
How can we improve travel?
How can we better retain information?
2. Data Understanding - at this step, you need to move the questions from Business Understanding to data. You might already have data that could be used to answer the questions, or you might have to collect data to get at your questions of interest.

[Quiz + Notebook: A Look at the Data](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/A%20Look%20at%20the%20Data.ipynb)

When looking at the first two questions:

How to break into the field?
What are the placement and salaries for those who attended a coding bootcamp?
we did not need to do any predictive modeling. We only used descriptive and a little inferential statistics to retrieve the results.

Therefore, all steps of CRISP-DM were not necessary for these first two questions. The process would look closer to the following:

1. Business Understanding

2. Data Understanding

3. Prepare Data

4. Evaluate the Results

5. Deploy

However, for the last two questions:

How well can we predict an individual's salary? What aspects correlate well to salary?

How well can we predict an individual's job satisfaction? What aspects correlate well to job satisfaction?

We will need to use a predictive model. We will need to pick up at step 3 to answer these two questions, so let's get started. The process for answering these last two questions will follow the full 6 steps shown here.

1. Business Understanding

2. Data Understanding

3. Prepare Data

4. Model Data

5. Evaluate the Results

6. Deploy



Business and Data Understanding
Business Questions
How do I break into the field?
What are the placement and salaries of those who attended a coding bootcamp?
How well can we predict an individual's salary? What aspects correlate well to salary?
How well can we predict an individual's job satisfaction? What aspects correlate well to job satisfaction?
Data Understanding
You will be using the Stackoverflow survey data to get some insight into each of these questions. In the rest of the lesson, you can work along with me to answer these questions, or you can take your own approach to see if the conclusions you draw are similar to those you would find throughout this lesson.

The CRISP-DM Process (Cross Industry Process for Data Mining)
We have now defined the questions we want to answer and had a look through the data available to find the answers, that is, we have looked at the first two steps here:

1. Business Understanding

2. Data Understanding

We can now look at the third step of the process:

3. Prepare Data

Luckily stackoverflow has already collected the data for us. However, we still need to wrangle the data in a way for us to answer our questions. The wrangling and cleaning process is said to take 80% of the time of the data analysis process. You will see that will hold true through this lesson, as a majority of the remaining parts of this lesson will be around basic data wrangling strategies.

We will discuss the advantages and disadvantages of the strategies discussed in this lesson.

[Notebook + Quiz: How To Break Into the Field](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/How%20To%20Break%20Into%20the%20Field.ipynb)

[Notebook + Quiz: Job Satisfaction](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/Job%20Satisfaction.ipynb)

When looking at the first two questions:

How to break into the field?
What are the placement and salaries for those who attended a coding bootcamp?
we did not need to do any predictive modeling. We only used descriptive and a little inferential statistics to retrieve the results.

Therefore, all steps of CRISP-DM were not necessary for these first two questions. CRISP-DM states 6 steps:

1. Business Understanding

2. Data Understanding

3. Prepare Data

4. Data Modeling

5. Evaluate the Results

6. Deploy

For these first two questions, we did not need step 4. In the previous notebooks, you performed steps 3 and 5 without needing step 4 at all. A lot of the hype in data science, artificial intelligence, and deep learning is integrated into step 4, but there are still plenty of questions to be answered not using machine learning, artificial intelligence, and deep learning.

All Data Science Problems Involve
Curiosity.

The right data.

A tool of some kind (Python, Tableau, Excel, R, etc.) used to find a solution (You could use your head, but that would be inefficient with the massive amounts of data being generated in the world today).

Well communicated or deployed solution.
Extra Useful Tools to Know But That Are NOT Necessary for ALL Projects
Deep Learning
Fancy machine learning algorithms
With that, you will be getting a more in depth look at these items, but it is worth mentioning (given the massive amount of hype) that they do not solve all the problems. Deep learning cannot turn bad data into good conclusions. Or bad questions into amazing results.

In the modeling section, you will learn that step three of CRISP-DM is essential to getting the most out of your data. In this case, we are interested in using any of the variables we can from the dataset to predict an individual's salary.

The variables we use to predict are commonly called X (or an X matrix). The column we are interested in predicting is commonly called y (or the response vector).

In this case X is all the variables in the dataset that are not salary, while y is the salary column in the dataset.

On the next page, you will see what happens when we try to use sklearn to fit a model to the data, and we will do some work to get useful predictions out of our sklearn model.

[Notebook + Quiz: What Happened?](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/What%20Happened.ipynb)

### Working With Missing Values

There are two main 'pain' points for passing data to machine learning models in sklearn:

Missing Values
Categorical Values
Sklearn does not know how you want to treat missing values or categorical variables, and there are lots of methods for working with each. For this lesson, we will look at common, quick fixes. These methods help you get your models into production quickly, but thoughtful treatment of missing values and categorical variables should be done to remove bias and improve predictions over time.

Three strategies for working with missing values include:

We can remove (or “drop”) the rows or columns holding the missing values.
We can impute the missing values.
We can build models that work around them, and only use the information provided.

Though dropping rows and/or columns holding missing values is quite easy to do using numpy and pandas, it is often not appropriate.

Understanding why the data is missing is important before dropping these rows and columns. In this video you saw a number of situations in which dropping values was not a good idea. These included

Dropping data values associated with the effort or time an individual put into a survey.
Dropping data values associated with sensitive information.
In either of these cases, the missing values hold information. A quick removal of the rows or columns associated with these missing values would remove missing data that could be used to better inform models.

Instead of removing these values, we might keep track of the missing values using indicator values, or counts associated with how many questions an individual skipped.

### Removing Data - When Is It OK?

In the last video, you saw cases in which dropping rows or columns associated with missing values would not be a good idea. There are other cases in which dropping rows or columns associated with missing values would be okay.

A few instances in which dropping a row might be okay are:

Dropping missing data associated with mechanical failures.
The missing data is in a column that you are interested in predicting.
Other cases when you should consider dropping data that are not associated with missing data:

Dropping columns with no variability in the data.
Dropping data associated with information that you know is not correct.
In handling removing data, you should think more about why is this missing or why is this data incorrectly input to see if an alternative solution might be used than dropping the values.

One common strategy for working with missing data is to understand the proportion of a column that is missing. If a large proportion of a column is missing data, this is a reason to consider dropping it.

There are easy ways using pandas to create dummy variables to track the missing values, so you can see if these missing values actually hold information (regardless of the proportion that are missing) before choosing to remove a full column.

[Notebook + Quiz: Removing Values](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/Removing%20Values.ipynb)

[Notebook + Quiz: Removing Data Part II](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/Removing%20Data%20Part%20II.ipynb)

### Imputing Missing Values

Imputation is likely the most common method for working with missing values for any data science team. The methods shown here included the frequently used methods of imputing the mean, median, or mode of a column into the missing values for the column.

There are many advanced techniques for imputing missing values including using machine learning and bayesian statistical approaches. This could be techniques as simple as using k-nearest neighbors to find the features that are most similar, and using the values those features have to fill in values that are missing or complex methods like those in the very popular AMELIA library.

Regardless your imputation approach, you should be very cautious of the BIAS you are imputing into any model that uses these imputed values. Though imputing values is very common, and often leads to better predictive power in machine learning models, it can lead to over generalizations. In extremely advanced techniques in Data Science, this can even mean ethical implications. Machines can only 'learn' from the data they are provided. If you provide biased data (due to imputation, poor data collection, etc.), it should be no surprise, you will achieve results that are biased.

[Notebook + Quiz: Imputation Methods & Resources](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/Imputation%20Methods%20and%20Resources%20-.ipynb)

[Notebook + Quiz: Imputing Values](https://github.com/chloehuang123/udacity-nano-data-scientist/blob/main/CRISP_DM/Imputing%20Values.ipynb)
