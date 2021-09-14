## NLP MVP

After preprocessing the text which includes the hotel star rating, hotel description, and area description with a dataset of 5 cities, I built my baseline hotel recommender using SVD with 1-gram and calculated cosine similarity to provide the top 5 recommendations.  Among the 5 recommendations, top 3 hotels have similiar star rating, hotel description, and area description as the input hotel, but the other 2 have different content in those three areas.

Next, I will build the recommender with the following ways and see if the recommendation improves:

* SVD with 1-gram, bi-gram, and tri-gram with the same text (star rating, hotel description, and area description)

* SVD with 1-gram, bi-gram, and tri-gram with text of area description plus star rating.