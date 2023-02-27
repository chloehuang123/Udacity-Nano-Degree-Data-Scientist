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


