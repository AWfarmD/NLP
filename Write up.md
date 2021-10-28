# NLP Write-Up

### Abstract

The goal of this project was to create a content based hotel recommendation system where top 5 similar hotels will be recommended to the user based on the hotel he/she is originally interested in. Specifically, the recommended hotels will be in the "You may also like..." section once the user searches the hotel (input hotel) in the search box.  I worked with the data scrapped from Expedia.com, using truncated SVD and NMF to achieve this goal.

### Design

Sometimes the hotel you are interested in staying for your vacation may be not availabe.  When this happens, it would be convenient if the website shows other hotels with similar star ratings, amenities, and area attractions, so you do not have to spend time researching them.

### Data

The star ratings, hotel descriptions, and area descriptions of 1,964 hotels in Chicago, New York City, Seattle, San Francisco, Los Angeles (These are cities of interest), and cities in the vacinity aroud cities of interest were scraped from Expedia.com. After cleaning and adding in missing values, the same 1,964 observations were used for preprocessing and topic modeling. However, after the first attempt of building the recommender, certain obervations were dropped, and only about 1,000 observations were left for further topic modeling (Process detailed below).

### Algorithms

After cleaning the data, I then preprocessed the corpus by making all text lower case and removing punctuation, numbers, stop words, and special characters (ex. "–"), and tfidf vecterizer were used to create a sparse matrix.

**Truncated Singular Value Decomposition**

Truncated SVD was tried first to perform topic modeling, and I set to obtain five topics. When I saw the terms in each of the generated five topics, I realized all the hotel descriptions were very smilier and general; having terms talking about free Wifi, TV, air condition, parking, etc. I then decided to drop the hotel description, so there could be more specific and meaningful topics. 

While performing more topic modeling, I realized the area attraction descriptions for each of the hotel used similar format and terms. Examples were they all talked about outdoor activities, and used same terms like "adventures", "kayaking", "activity", and "golfing", and they also talked about shopping and night life, and used same terms like "shopping", "clubs", and "night". All these terms showed up in all five topics, so I was not able to obtain meaningful topics. Therefore, I removed all these terms from the corpus. 

During the subsequent topic modeling process, I also realized pieces of attraction names that were common in all the cities appeared in some topics (ex. "market" from "Pike Place Market" in Seattle and "market" from "Grand Central Market" in Los Angeles), and were muddying the topics generated, so I used MWETokenizer and word_tokenize to create several compounded attraction names (ex. Paramount Studios, Millennium Park, Pike Place Market, etc) to resolve this issue.

After creating compounded attraction names and then perform topic modeling, five topics each contained a city of interest's name and its attractions were obtained. However, upon closer inspection, Topic 1 which was New York City and its attractions had the term, "San Francisco" in it, and Topic 3 which was Chicago and its attractions had "Seattle" in it. I thought there might be some common attraction terms among these cities that were muddying the topics, so I added more compounded attraction terms for each of the four cities in order to make each topic as a distinct city and its attractions. However, that never happened.

I went ahead and built the recommender, and two out of the five recommendations were always way off.  And if the input hotel is located in a city in the vicinity of cities of interest, all five recommendations would be off.  It was most likely because the five topics generated were cities of interest and attractions in these cities, so whenever the input hotel is located in a city that is not one of those five cities, the system was not able to generate an accurate recommendation. So I decided to drop the hotels located outside of the cities of interest, and worked with the remaining 995 observations.

After the drop, I tried the recommender again. This time, all five recommendations were spot on.  However, upon other tries, I realized the current recommendation system were producing extreme results. It either provided excellent recommendations where the five recommended hotels had similar area attractions and star ratings, or those that did not make any sense at all.  

**Non-Negative Matrix Factorization**

I then decided to use NMF to build the recommender.

Same preprocessing such as making all text lower case and removing punctuation, numbers, stop words, and special characters (ex: "–") were done on the corpus. The obervations only included cities of interest, and tfidf vecterizer was used to create a sparse matrix.

I did a test-run topic modeling with NMF without removing the common terms apearing in the area attraction description ( "adventures", "golfing", "shopping", and "clubs" etc. mentioned above) and without adding compouned attraction terms ("Pike Market Place" and "Millennium Park" etc. mentioned above), and it produced five topics each as one city of interest and its attractions. I then built a recommender with these topics, and it gave a more mixed result comparing to the one with truncated SVD; out of the five recommendations, some had the same attractions and star ratings, some had the same attractions but different star ratings or vice versa, and some were completely off.

I chose the recommender with NMF as the final recommendation system because it gave more mixed results rather than extreme results from the truncated SVD, so the users will be able to find some useful information out of the five recommendations rather than having all five wrong at some time.

### Tools

* Beautiful Soup and Selenium for data scraping
* Pandas for data cleaning
* Python text processing libraries (NLTK and scikit-learn) for data preprocessing

### Communication

Findings and slides will be presented.

