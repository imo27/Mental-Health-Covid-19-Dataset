# Mental-Health-Covid-19-Mental-Health
## Nawaf Alhumadi, Ifeanyi Osuchukwu
Covid-19 Mental Health Dataset is a dataset derived from twitter and its composition is made from the tweets of many users concerning topics related to mental health during the current Covid-19 Global Pandemic. 

### Covid-19 Mental Health Dataset
Using Snscrape we were able to acquire data by collecting tweets involving the association of mental health and COVID-19 from  nearly the last two months . Snscrape is a scraper for social networking services (SNS). It scrapes things like user profiles, hashtags, or searches and returns the discovered items.

Taking into consideration the recently growing focus on the importance of mental health in western society, as well as the fact that COVID-19 is still heavily impacting our day to day lives; We wanted to create a dataset that could help uncover how COVID has directly impacted the mental health a of university students and potentially how their attitudes on mental health may or may not have changed during these times. COVID-19 has fundamentally changed the way we interact with one another, which in turn has affected our learning environments and our social interactions. As a group, we believe that creating datasets pertaining to this topic would be of immense value. Our hope is that this data would be of interest to mental health organizations that have a particular focus on university students and mental health topics concerning young adults in general. This data could possibly attract the many companies operating in the self-care, therapy, and meditation space such as Talkspace, Headspace, and Better Help. Many of which are already utilizing social media for monitoring vulnerable individuals who post status suggesting wanting to harm themselves. Social media's role in mental research continues to grow. In a study conducted by Eichstaedt et al., using data from consenting Facebook users’ researchers were able to predict future occurrences of depression in their medical records. This was done by analyzing language predictive of depression from users. The study suggests that an analysis of social media data could be used to screen consenting individuals for depression. https://www.pnas.org/content/115/44/11203 . It’s our hope that our dataset could be further analyzed and produce insights into how covid-19 has affected mental health in young adults. Across the country universities have spent and acquired resources to better accommodate students with mental health services. This kind of data could also attract schools as they too would want to understand how COVID may be affecting their students.



## Current Usage Instructions
The datasets created through this program can be used for future sentiment analysis and visualization. The program can be altered to cover any topic of interest and for any given time period, by changing the query parameters. The program has an emphasis on text data from any given tweet we have tools in our program that tokenize tweets by sentence and produces a word frequency count. 

### Necessary Installations/Setups:
###### Python: need version 3.0 or later.
This project utilized Jupyter Notebooks from Anaconda
 The following dependencies are needed:
 
 pip install spacy
 !python -m spacy download en_core_web_sm
 !pip install git+https://github.com/JustAnotherArchivist/snscrape.git
 import snscrape.modules.twitter as sntwitter
!pip install pymongo[srv]
 conda install git

 Make sure all Python Modules are imported:
 json, csv, uuid, config(local py file), os, logging, re
 pymongo subprocess, pandas, numpy, spacy, from IPython.display (display_javascript,
 display_html,display, HTML) from datetime(datetime, date, time, timedelta) from pathlib(Path)
 from pprint(pprint) from collections(Counter) snscrape.modules.twitter

 Use command prompt to install packages: 
 Your python engine may be called "python" or "py". take "py" for example, below command lines to install some of the packages required:

 py -m pip install "pymongo"

 py -m pip install "numpy"

 py -m pip install "spacy"

 py -m pip install "IPython.display"

 py -m pip install "datetime"

 py -m pip install "pathlib"

 py -m pip install "collections"

 py -m pip install "pandas"


###### MongoDB Database:
Users do not have to utilize a MongoDB Database. Other avenues can be used to store tweet data, such as csv and json files or other database programs like MYSQL. 
However, we felt MongoDB was best for this project and is really easy to use.
MongoDB was used to store our data acquired from twitter. MongoDB works well for  json formatted collections. 
No installation is needed: However click this link to learn how to setup a free account and start a cluster: https://www.youtube.com/watch?v=rPqRyYJmx2g
Also, for more information on pymongo and connecting python to MongoDB refer to https://pymongo.readthedocs.io/en/stable/ and https://www.mongodb.com/blog/post/getting-started-with-python-and-mongodb

###### Files
config.py: This file holds are access codes and information necessary to log into our Atlas MongoDB Database. This file is imported in as module for security purposes.
data_distrubution folder: This folder will house the proccessed and raw data csv files.
PROCESSED_DATA.csv: This file is the proccessed data from our code that will be analyzed.
RAW_DATA.csv: This file is the raw data scraped from twitter. 
log.log: This file is a log containing information on how the code is running. 
Group7_final_project.iynb: This file houses the python logic to run our code which acquires and processes tweets using Snscrape and places the processed data into a python dataframe. 
Example_Code.iynb: This file is the the same code used to run our code but with examples and markdowns used to better understand our code.It also contains the ReadMe.md contents as well.  
data_profile_report.html: This file profiles our data and its values. 
Miro_Presentation.pdf: This file is our presentation of our project. Please note we have made major changes to how we acquire tweets and we don't utilize twython.


######  Functions
>The term "tweet" is synonymous for a json object or a data dictionary.

1:flatten_dict(): Twitter raw data comes in json format with nested keys and values. This function flattens are dictionary, so we can access all of the keys and values from our tweet. The argument for the function is a nested dictionary(tweet).
 2:filter_tweet(): Utilizes the flatten_dict() function and retrieves all the keys that are specified in our filter_list variable. This is the actual information fields we want from a given tweet from Snscrape. The arguments are (tweets and key list that a user desires).
 3:remove_links_from_tweet_content(): This function removes hyperlinks,"@", and RT from the content field of tweet. Function argument is a tweet.
 4:split_content_into_sents(): Tokenizes the content field of a tweet into sentences. The argument is the content key from a tweet. 
 5:word_freq(): Utilizes the counter function from the collections module and counts the words in a sentence that is not a stop word or punction. The argument is the content key of a tweet. 
 6:common_words(): Also utilizes the counter function and the most common method to return the 5 most common words in a given tweet. The argument is the content key of a tweet. 
 7:process_tweet(): This function utilizes functions(2-6) to produces our processed tweet. We add three new keys to our dictionary (sents, word_freq, common_words). The argument for the function is a tweet object from Snscrape.
 8:insert_tweet_to_database(): This function places the processed tweet into our MongoDB database. The arguments are tweets and the name of the collection where the tweets will be stored. 
 9:load_tweets(): This function is how we use Snscrape module to scrape twitter for desired tweets. The arguments are a query which contains the search phrase a user desires to search on twitter. Next is the since date and the until date.  The function also takes language arguments as well as the number of results desired. The last argument is the name of MongoDB collection you want the data to be uploaded to. This function utilizes the process_tweet function and insert_tweet_to_database. 
 
 
 ## Considerations for the Dataset
 We have two collections in our MongoDB database "RAW_DATA" and "PROCESSED_DATA". We upload tweets based on their tweet id key so we don't have duplicate tweets in our datasets. The names of our collections are just how they sound the "RAW_DATA" contains tweets directly from Snscrape, where as the "PROCESSED_DATA" collections contains only filtered tweets with our target data that is loaded into a python dataframe. 
 
 We use 9 key phrases to target our tweets data. We wanted to make sure our tweets had some level of relevancy to our topic. So here lies a potential limitation of our dataset. However,
 more phrases can be used to produce data of interest. We have nearly 10,000 thousand tweets collected over two months. Ideally, we would want more for future sentiment analysis.So, we would also increase the range from when we started collecting tweets.  Originally our hope was to focus on the young adult demographic however, not all tweets and twitter at large doesn't provide that kind of information. We also hoped to have location-based data, but again if a user has their geolocation data turned off we can’t collect it. For future updates to the project we would like to implement more phrases as well as having the program run automatically at desired time intervals. The information we pulled from each tweet can be found in our filter_list variable in addition to our created keys (sents, word_freq, and  common_words).  We believe this information was relevant for each tweet and can be used for further analysis.  
 When running our code be sure to limit the max amount of results, we find that it takes about 9 seconds to retrieve 50 tweets so scale that with caution. When making changes to the program cell 5 contains major variables that affect the query parameters so be sure to make them how you want. 
 ## Distribution 
 We are going to export our data into a csv file. With some more refinements we may choose to publish this dataset to our own personal github accounts. And perhaps with more experience we can actually try to analyze the data ourselves.
