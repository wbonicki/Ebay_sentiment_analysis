## Reviews sentiment analysis

__Description__
The goal of the project was to build a model that can determine a sentiment of a review. The sentiments were of three kinds: positive, negative and neutral.
The kind of a review sentiment results from a rating given by a customer: 1,2 is considered as negative, 3 as neutral and 4,5 as positive.
The project preceeded in two steps:  

# 1. Data extraction

The data were collected from Ebay e-commerce website and data collection was carried out twice (at two different times). 

Functions for data extracion are in _data_extraction.ipynb_ and the process of data collection is shown below.

![alt text](https://raw.githubusercontent.com/wbonicki/Ebay_sentiment_analysis/master/screeny/search_results.jpg)

List of search words are given by a user. The script looks for products with reviews for every given search word for _n_ pages.
Next it downloads all the ratings and reviews and puts them in pandas dataframe.

# 2. Model for sentiment analysis

Because almost 93% of the reviews are positive the classification task is considered as imbalanced classes problem. 
On the whole two cases were considered.
 - The first case:
only positive and negative reviews were taken into account (binary classification - neutral reviews were not part of fitting a model).
This case resulted from neutral reviews ambiguity (examples are shown in jupyternotebook).
 - The second case 
all reviews were taken into account and it was multiclass problem. 

The figure below shows a general way of proceeding for both cases. 


![alt text](https://raw.githubusercontent.com/wbonicki/bitcoin-price-prediction/master/TS.jpg)

Two aproaches were tested: 
 - classical machine learning (algorithms like SupportVectorMachine, DecisionsTree, LogisticRegression etc.
 - deep learning: recurrent neural networks with pretrained word embeddings (glove)

The models were evaluated by precision, recall and accuracy scores.

## Results
