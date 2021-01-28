# Reviews sentiment analysis

## Description

The goal of the project was to build a model that can determine a sentiment of a review. The sentiments were of three kinds: positive, negative and neutral.
The kind of a review sentiment results from a rating given by a customer: 1,2 is considered as negative, 3 as neutral and 4,5 as positive.
The project preceeded in two steps:  

# 1. Data extraction

The data were collected from Ebay e-commerce website and data collection was carried out twice (at two different times). 

Functions for data extracion are in `Data_extraction.ipynb` and the process of data collection is shown below.

List of search words are given by a user. The script looks for products with reviews for every given search word for _n_ pages.

![alt text](https://raw.githubusercontent.com/wbonicki/Ebay_sentiment_analysis/master/screeny/search_results.jpg)

When a product with reviews is found the scrip downloads all the ratings and reviews and puts them in pandas dataframe.

![alt text](https://raw.githubusercontent.com/wbonicki/Ebay_sentiment_analysis/master/screeny/search_results2.jpg)

# 2. Model for sentiment analysis

Because almost 93% of the reviews were positive the classification task was considered as imbalanced classes problem. 
In general two cases were considered.
 - The first case:
only positive and negative reviews were taken into account (binary classification - neutral reviews were not part of fitting a model).
This case resulted from neutral reviews ambiguity (examples are shown in jupyternotebook).
 - The second case 
all reviews were taken into account and it was multiclass problem. 

Two aproaches were tested: 
 - classic machine learning (algorithms like SupportVectorMachine, DecisionsTree, LogisticRegression etc.)
 - deep learning: recurrent neural networks with pretrained word embeddings (glove)

The test set used for final evaluation was 20% of all the reviews

The figure below shows a general way of proceeding for both cases. 

![alt text](https://raw.githubusercontent.com/wbonicki/Ebay_sentiment_analysis/master/screeny/schema.jpg)

Model performance was evaluated by precision, recall and accuracy scores for minor classes.

## Results

Support Vector Classifier turned out to be the best model for boths cases. It outperformed neural networks as well.


# Files description
`Classic_Machine_Learning.ipynb` - jupyter notebook file with classic machine learning approach

`Data_extraction.ipynb` -  jupyter notebook file with function for downloading reviews from Ebay

`Neural_Networks.ipynb` - jupyter notebook file with neural networks

`data_analysis.ipynb` - jupyter notebook file with data analysis

`Data_ML.csv` - a csv file where reviews are cleaned and prepared for machine learning modelling

`Data_NN.csv` - a csv file where reviews are cleaned and prepared for neural networks modelling

`ebay_reviews.csv` - the first part of raw reviews

`ebay_reviews30122020.csv` - the second part of raw reviews