
# H1N1 Vaccination Analysis Read Me

October 2023

Andrew Hendricks (andrewhhendricks@gmail.com)

Non-Technical Presentation: https://docs.google.com/presentation/d/1DO3q7NLQlQhLXU-m109f83YQLVI_L7PI/edit?usp=sharing&ouid=106491021188736703963&rtpof=true&sd=true


## Overview

Whether in terms of lives lost, mental health, or the economy, the devastation of the COVID-19 pandemic has been colossal.

The severity of the COVID-19 crisis highlighted the importance of understanding vaccination patterns. Once scientists developed the vaccine and companies were able to produce it at scale, we saw how influential factors like beliefs, opinions, and politics became in the effort to vaccinate the public.

Deepening our understanding of the specifics of how an individual's background, opinions, and behaviors relate to whether they decide to get vaccinated can help health officials make data-driven decisions around the most effective ways to protect the public from future pandemics. In this project, I use data from a past pandemic, the H1N1 pandemic of 2009, to create a model that uses information from the National 2009 H1N1 Flu Survey to predict whether people got H1N1 vaccines. I conclude the analysis by offering three recommendations for how public health officials can support future public health efforts.

### Business Problem and Data

The main stakeholder for this project would be public health experts. The business problem is developing a model that predicts whether an individual took the H1N1 vaccine based on their responses to the survey questions.  Because of the nature of the problem, my model predicts whether someone will get an H1N1 vaccine, and I use accuracy as my most important classification metric. There is no domain-specific need for the model to do a better job at avoiding false positives or false negatives, so my goal is to create a model that is as accurate as I can make it.

This analysis is based on the prompt from the Driven Data Flu Shot Competition. The data for the analysis was hosted there as well. The survey that the data comes from was conducted during 2009. The survey was conducted using random digit dialing and targeted all people ages 6 months and older. The survey contained over 26,000 records.

All of the columns in the data set could be treated as categoricals. After data cleaning, I used one hot encoding on all non-binary columns. I used a simple imputer set to most frequent to handle null values.


## Modeling

For my model, class 1 was that someone got the H1N1 vaccine and class 0 was that they did not. I used test train split to train and test my model and used pipelines to handle one hot encoding and simple imputing.  My most important classification metric was the accuracy score, but I also reviewed precision, recall, F1, ROC AUC, and log loss when evaluating the preformance of my models.

My first model was a dummy classifier. The majority class within the data set was class zero at 79%, so the classifier had a 79% accuracy score.

My second model used a logistic regression on all columns.

My third model used a logistic regression on columns that I selected after using lasso regularization on all columns to determine which variables had the weakest impact.

My final model used polynomial features and ridge regularization on the selected columns from the third model.


## Evaluation

Overall, the most accurate models were the first model and the second model, which had accuracy scores of 84%. These models also had the lowest log loss and the highest precision and recall scores. The next best was the third model, which had an accuracy score of 83%. All of these models beat the baseline dummy classifier, which had an accuracy score of 79%. 

To create my recommendations, I used investigated the strength of the coefficients for each variable from my first model. The first and second models had virtually identical performance in terms of all the classification metrics. I decided to use the first model because it was more inclusive.

Because the coefficients represented log odds, which have a low level of interpretability, I decided to convert them to probabilities. I used np.exp to transform the log odds into odds and then converted the odds into probabilities. This allowed me to use what I felt to be a more interpretable metric when communicating with a non-technical audience.


## Conclusion

Based on my model, a doctor recommendation was the variable associated with the strongest increase in the probability that someone would take the vaccine. Further, survey questions about the risk of H1N1, the vaccine's effectiveness, and the likelihood of getting sick from the vaccine all were associated with strong shifts in the probability of someone getting the vaccine. When people responded that the risk of the virus was low, that response was associated with a 57% decrease in the probability of them getting the vaccine; when people responded that the risk of the virus was high, that response was associated with an 83% increase in the probability of them getting a vaccine. Finally, generally healthy behaviors like wearing a face mask were also associated with an increase in the probability that someone would get the vaccine.

Based on these findings, my recommendations to public health officials would be: 1: Doctors should be vocal supporters of vaccines when pandemics are going on. 2: Fight the war of opinion by messaging on pandemic risks, vaccine effectiveness, and vaccine safety. 3: Promote generally healthy behaviors like frequently washing hands when pandemics are not occurring to increase health consciousness.
