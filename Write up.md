## Content Based Hotel Recommendation System

**Abstract**

The goal of this project was to create a hotel recommendation system where top 5 similiar hotels will be recommended to the user based on the hotel he/she is originally interested in.  Specifically, the recommended hotels will be in the "You may also like..." section once the user searches the hotel in the search box.  I worked with the data scrapped from Expedia.com, using SVD and NMF along with calculated cosine similarity to achieve this goal.

**Design**

Sometimes the hotel you are interested in staying for your vacation may be not availabe.  When this happens, it would be convenient if the website shows other hotels with similiar star ratings, amenities, and area attractions, so you do not have to spend time researching them.

**Data**

The star ratings, hotel descriptions, and area descriptions of 1,964 hotels in Chicago, New York City, Seattle, San Francisco, Los Angeles, and cities in the vacinity were scraped from Expedia.com.  After cleaning and adding in missing values, the same 1,964 observations were used for preprocessing and modeling.  

However, after the first attempt of building the recommender, two out of the five recommendations were almost always off.  And if the hotel is in a city in the vicinity, all five recommendations would be off.  So I decided to drop the hotels located outside of the cities of interest, and worked with 995 observations in the second round.

**Algorithms**

SVD was tried first to perform dimensionality reduction.  When I saw the terms in each of the generated five topics, I realized each of the hotel description is very smilier; talking about free Wifi, TV, air condition, parking, etc.  I decided to drop the hotel description text, so it won't affect the reasult, and only worked with text from the star rating and area descriptions.  NMF was later used to develop the second model with the same text of star rating and area descriptions.  Calculated cosine similarity for both models were used to provide the top five recommendations.

**Tools**

* Beautiful Soup and Selenium for data scraping
* Pandas for data cleaning
* Python text processing libraries (NLTK and scimitar-learn) for data preprocessing

**Communication**

Findings and slides will be presented.

