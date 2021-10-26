# NLP MVP

After cleaning the data, I preprocessed the corpus by making all text lower case and removing punctuation, numbers, stop words, and special characters, and tfidf vecterizer was used to create a sparse matrix.  

Truncated SVD was used to perform topic modeling, and was set to create five topics.  Af this point, I still could not find meaningful topics.  All topics contain general terms like "parking", "free", "wifi", "adventures", "activity", "cultural", and "experience" etc.  I am suspecting this is because the descriptions about the amenities of the hotels and about the attractions around the hotels are written in similiar format and contain the same terms.

My next step is to read some of the descriptions mentioned above, and see if they are indeed written in simliar format and contain the same terms, and I will remove some of these terms or potentially not using the descriptions to see if this will create more meaningful topics.

