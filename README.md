# Monitoring Daily Tweets Project

Across the years, Twitter has become an important source of information about a diverse range of topics, ranging from entertainment, politics and consumer habits, to personal views about the contemporary, everyday people´s life. Maybe without search for it, Twitter is the de facto memoir of modern times. Among the potential data use cases, either be social studies or marketing research, if we want to take a
look to the data stored in the vas amount of tweets made everyday around the world, things can get a little messy (How can we scrape the tweets?, How to filter them to get the data of interest? How do we get other important data, like the location or user stats?). This project aims to provide an analytics workflow for tweets, encompassing the whole process: from retrieving the tweets about a specific topic and date, the preparation of the data and preliminary exploration, to text processing algorithms like sentiment analysis, clustering technics and word shift analysis.

In order to show the workflow in action, I choose to apply it over a current topic: covid 19 tweets. The notebook in this repository shows the complete workflow developed and the analysis of the results obtained. If you think this workflow is useful for your own purposes, please feel free to change the topic and/or the parameters of the tweets retrieving part. The idea behind this project is to bring a ready to use tool for analyzing Twitter content on a regular basis.  

All the covid19 data files and data processing are contained in this repository.

Fundamentally, this project was developed in six stages:
1. Tweets recollection through the Twitter API.  
2. Data preparation.
3. Exploratory Data Analysis.
4. Tweets Geographic Location.
5. LDA Clustering.
6. Extraction of Sentiment Coefficients.
7. Word Shift Analysis.

For any question, suggestion or discrepancy, feel free to write me at german.pinzon@davivienda.com


## Libraries needed:

You can run this project in a Python 3.7 environment with the following modules installed:

- pandas (1.0.1)
- numpy (1.18.1)
- re (2020.7.14)
- tweepy (3.9.0)
- seaborn (0.10.1)
- sklearn (0.19.1)
- nltk (3.4.5)
- plotly (4.13.0)
- pyLDAvis (2.1.2)
- google-cloud-language (1.3.0)

If you want to install these modules in an environment, you can run the installation of **requirements.txt** file in your environment.

**Note:** In order to connect with the Twitter API for retrieving the data, it is necessary to have Twitter API keys for authentication. In https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens you can learn how to get them for free. 

Also, for performing the sentiment proccessing of tweets, I make use of the Google Cloud Sentiment Analysis micro service, that also needs its own credentials. You can get access to the API (You can process 5000 texts monthly for free). More information on https://cloud.google.com/natural-language/docs/analyzing-sentiment.

However, if you don't want to run these external connections to the Twitter API and Google Cloud Sentiment Analysis, there are already the tweets database (**covid_tweets_10000.csv**) and the tweets database with sentiments coefficients computed (**covid_tweets_10000_sentiments.csv**) already in this repo for loading. 


## Repository Contents:
        
- covid_tweets.ipynb:

- covid_tweets_10000.csv: 
   
- covid_tweets_10000_sentiments.csv:

- requirements.txt: Set of Python modules needed to run this project.

- README.md


## User Instructions: 

- If you want to see the full covid tweets workflow, you can run in order all the cells in the **covid_tweets.ipynb** notebook, provided you have the Twitter API and Google Cloud credentials.

- If you just want the analyze the data, without retrieving the tweets and perform sentiment extraction, you can run the cells that load the csv's in the repo and go directly to the sections **2**, **3**, **4**, **5** and **7** in the notebook.

- Finally, if you want to apply the whole workflow over your own topics/parameters, you can modify the section 1 of the notebook. Within it are more specific instructions.


## Summary:

- In the data preparation stage, I found 41 duplicate rows that were dropped from the final table in the database. On the other hand, I think that the 'original' column in the preliminary message data table (the message in its original language) is not relevant for the developed classification tool (besides not all of the messages have their correspondent original language version, only 10184 of them), so I dropped this column from the final table too. 
- The final database table have 138 messages that have no classification. Thus, these messages were filtered for the train and test set of the ML text classification model. However, these messages were saved in another, alternative dataframe called 'df_test' within the ML training script, if it is required for model testing in later validations.
- I also converted the classification training values to binary in the process data script, due to some "2"s were discovered in the original database table.
- The tokenization preprocessing step gets rid of english stopwords and applies lemmatization to every message string.
- Train/Test training sets rate was 80/20.
- The model was trained through a grid search technique, with 20 alternatives feeding 8 different parameters of the ML Pipeline, ranging from the n_grams and max permitted features in the Count Vectorizer preprocessing stage to the number of neighbors in the K-Neighbors Classifier used in the Scikit Learn's Multioutput Classifier. Of course, due to the fact this training took a lot of time, the final version of the Grid Search you will going to find in this repo is a simplified version with the best parameters found.
- I also explored a Random Forests Classifier with a custom made text lenght extractor sklearn estimator, with similar performance results compared to the shown model.
- The worst results in performance were in the 'related', 'aid_related', 'weather_related' and 'direct_report' categories. A summary of the model performance can be seen in the verbose of 'train_classifier.py' script run.
- Because the dataset is imbalanced, I recommend special attention to the F1-score metric, which balances how well the model classifies positive cases and the fraction of positive cases within a category.
- Most of the disaster messages come from news reports, followed by direct aid request messages and social media posts (as you can see in the web dashboard).
- The vast majority of messages are aid requests. Less than 3% are aid offerings (as you can see in the web dashboard).
- Earthquakes, storms and floods are the most frequent natural disasters identified in the dataset (as you can see in the web dashboard).


## Acknowlegdments:

I want to thank Gabriel Preda for gave me the instructions on using the Twitter API. Also I want to thank the guys that develop the shifterator module and Ben Mabey that is the master behind the development of the PYLDAvis package.