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
- iso3166 (1.0.1)
- plotly (4.13.0)
- pyLDAvis (2.1.2)
- google-cloud-language (1.3.0)
- shifterator (0.1.2)

If you want to install these modules in an environment, you can run the installation of **requirements.txt** file in your environment.

**Note:** In order to connect with the Twitter API for retrieving the data, it is necessary to have Twitter API keys for authentication. In https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens you can learn how to get them for free. 

Also, for performing the sentiment proccessing of tweets, I make use of the Google Cloud Sentiment Analysis micro service, that also needs its own credentials. You can get access to the API (You can process 5000 texts monthly for free). More information on https://cloud.google.com/natural-language/docs/analyzing-sentiment.

However, if you don't want to run these external connections to the Twitter API and Google Cloud Sentiment Analysis, there are already the tweets databases (**covid_tweets_10000.csv** and **covid_tweets_10000_previous_day.csv**) and the tweets database with sentiments coefficients computed (**covid_tweets_10000_sentiments.csv** and **covid_tweets_10000_sentiments_previous_day.csv**) already in this repo for loading. 


## Repository Contents:
        
- **Daily_Tweets_Monitoring_Workflow.ipynb:** complete workflow.

- **covid_tweets_10000.csv:** Dataset of 10k December 10th tweets and data related. 

- **covid_tweets_10000_previous_week.csv:** Dataset of 10k December 4th tweets and data related.
   
- **covid_tweets_10000_sentiments.csv:** Dataset covid_tweets_10000.csv with sentiments coefficients computed. 

- **covid_tweets_10000_sentiments_previous_week.csv:** Dataset covid_tweets_10000_previous_day.csv with sentiments coefficients computed.

- **requirements.txt:** Set of Python modules needed to run this project.

- **README.md**


## User Instructions: 

- If you want to see the full covid tweets workflow, you can run in order all the cells in the **Daily_Tweets_Monitoring_Workflow.ipynb** notebook, provided you have the Twitter API and Google Cloud credentials.

- If you just want the analyze the data, without retrieving the tweets and perform sentiment extraction, you can run the cells that load the csv's in the repo (Section **3.1: Load datasets** and **6.2 Load Datasets (with 'sentiments' column)**) and go directly to the sections **2**, **3**, **4**, **5** and **7** in the notebook.

- Finally, if you want to apply the whole workflow over your own topics/parameters, you can modify the section 1 of the notebook. Within it, there are more specific instructions.

- It may be possible that the plots in sections **5** and **7** does not appear at first glance in the notebook. If this the case, please run the notebook according the instructions inside it in order to see them.


## COVID 19 Analysis Results Summary:

- Humans Rights day trend was identified, and it even get to the surface marketing stuff with little relation to the virus (PS5, XBOX, etc.)
- It seems that London midday is the most active time for tweeters.
- It seems that pandemics narratives are dominated by adhoc info services and news services.
- NDTV makes almost half of the total amount of tweets.
- The hashtags identified in section 3.5 play a relevant role in the found clusters.
- It seems that there are two main topics: The right one related to the overcome of the pandemic with terms like 'health' or 'vaccine' or the humans rights day previously identified (maybe the topic is 'optimism'?), and the smaller left one related to a more 'bad news' approach with words like 'deaths', or 'positive' (of course trump politics cannot be absent on this diagram).
- The alleged unrelated covid terms like 'ps5gamers' or 'xbox' belongs to the right cluster.
- There is no significant change in the narrative's emotions in this week.
- #humanrightsday hashtag push the most emotional tweets in Dec 10th compared to the past week.
- Hashtags like #covidvaccine or #allparty marked the differences in past week tweets compared to the Dec 10th tweets.
- It seems that this week were more active, both in positive and negative tweets. This is reflected in the global emotion content aggregate of the impact of these hashtags, that is, how much the words on each side of the axis on WordShift diagram push the emotional content of Dec 10th tweets, compared with the past week tweets on the Wordshift diagram.
- It seems that past week were more positive than Dec 10th, although the humans rights day were more relevant in positive interactions.
- There is a clearly increment in negative score margins in this week tweets. This may indicate rising controversies or more pugnacity on existing ones.
- On the neutral tweets we can identify a lot of terms that seem unrelated to the pandemics. This diagram looks like the 'normal' days comparative, were a variety of themes coexist in the top most popular topics.


## Acknowlegdments:

I want to thank Gabriel Preda for gave me the instructions on using the Twitter API. Also I want to thank Ryan J. Gallagher that develops the shifterator module, the guys behind the plotly package and Ben Mabey that is the master behind the development of the PYLDAvis package.