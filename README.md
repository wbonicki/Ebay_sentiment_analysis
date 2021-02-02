# Reviews sentiment analysis

## Description

The goal of the project was to build a model that can determine a sentiment of a review. The sentiments were of three kinds: positive, negative and neutral.
The kind of a review sentiment results from a rating given by a customer: 1,2 is considered as negative, 3 as neutral and 4,5 as positive.
The project preceeded in the following steps:  

## 1. Data extraction

The data were collected from Ebay e-commerce website and data collection was carried out twice (at two different times). 

Functions for data extracion are in `Data_extraction.ipynb` and the process of data collection is shown below.

List of search words are given by a user. The script looks for products with reviews for every given search word for _n_ pages.

![alt text](https://raw.githubusercontent.com/wbonicki/Ebay_sentiment_analysis/master/screeny/search_results.jpg)

When a product with reviews is found the scrip downloads all the ratings and reviews and puts them in pandas dataframe. __If a review is very long (_read full review_ option) the script does not download all content__ 

![alt text](https://raw.githubusercontent.com/wbonicki/Ebay_sentiment_analysis/master/screeny/search_results2.jpg)

## 2. Data analysis and preparation for modelling

The data was analized and word clouds for each sentiment group were built. Data was cleaned and  preprocessed for machine learning and neural network modelling using user defined transformers.
Because almost 93% of the reviews were positive the classification task was considered as imbalanced classes problem. 

## 3. Building model for sentiment analysis

In general two cases were considered.
 - The first case:
only positive and negative reviews were taken into account (binary classification - neutral reviews were not part of fitting a model).
This case resulted from neutral reviews ambiguity (examples are shown in `Data_analysis.ipynb` notebook).
 - The second case:
all reviews were taken into account and it was multiclass problem. 

Two aproaches were tested: 
 - classic machine learning (algorithms like SupportVectorMachine, DecisionsTree, LogisticRegression etc.)
 - deep learning: recurrent neural networks with pretrained word embeddings (glove - https://nlp.stanford.edu/projects/glove/)

The test set used for final evaluation was 20% of all the reviews

The schema below shows a general way of proceeding for both cases. 

![alt text](https://raw.githubusercontent.com/wbonicki/Ebay_sentiment_analysis/master/screeny/schema.jpg)

Model performance was evaluated by precision, recall and f1 scores for minor classes.

## 4. Best model performance evaluation

The best model (for both cases) was evaluated by classification report and confusion matrix. Misclassified reviews were examinated and some tests were carried out by giving their own reviews.

# Conclusion

The best model for both cases was support vector classifier with rbf kernel. 

|  BINARY CASE |Predicted negative|Predicted positive|
| ------------ |:----------------:|:----------------:|
|True negative |     387          |     18           |
|True positive |     40           |   8417           |


|  BINARY CASE   |precision|recall|f1-score|
| -------------- |:-------:|:----:|:------:|
|negative reviews|    0.91 | 0.96 |  0.93  |
|positive reviews|   >0.995|>0.995|  >0.995|


|  MULTICLASS CASE |Predicted negative|Predicted neutral |Predicted positive|
| ---------------- |:----------------:|:----------------:|:----------------:|
|True negative     |     360          |     2            | 43               |
|True neutral      |            13    |        235       |    41            |
|True positive     |       8          |      4           |     8445         |


|  MULTICLASS CASE |precision         |recall            |f1-score          |
| ---------------- |:----------------:|:----------------:|:----------------:|
|negative reviews  |     0.94         |     0.89         |  0.92            |
|neutral reviews   |           0.98   |      0.81        |     0.89         |
|positive reviews  |       0.99       |      >0.995      |     0.99         |


It happens that rating do not correspond to the review (many complains and a positive rating).
Neutral reviews are diversified and they are very ambiguous but the model handles such cases quite well.
It would be reasonable to create a model for predicting a sentiment regardless of customers rating - sometimes their ratings are misleading.
It should be emphasised that sentiment prediction can have different goals - sometimes detecting all negative reviews is more important and sometimes general accuracy.
Probabilty threshold and scoring depend on this issue. 


# Files description

`Data_extraction.ipynb` -  jupyter notebook file with function for downloading reviews from Ebay

`Data_analysis.ipynb` - jupyter notebook file with data analysis

`Classic_Machine_Learning.ipynb` - jupyter notebook file with classic machine learning approach

`Neural_Networks.ipynb` - jupyter notebook file with neural networks

`Final_model_summary.ipynb` - jupyter notebook file where the best models are evaluated

`Data_ML.csv` - csv file where reviews are cleaned and prepared for machine learning modelling

`Data_NN.csv` - csv file where reviews are cleaned and prepared for neural networks modelling

`ebay_reviews.csv` - the first part of raw reviews

`ebay_reviews30122020.csv` - the second part of raw reviews

`models` - folder with saved models