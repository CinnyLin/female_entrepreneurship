# Pipeline

## Data Collection

1. Getting raw data from Crunchbase --> [notebook_name]
- set data filters: xxx

2. Aggregating data with gender API --> [notebook_name]
- API: Namesor

## Data Preprocessing

3. Feature engineering --> `feature_eng`
- convert all data to numerical
- convert single and multi-categories rows to one-hot-encoded binary columns
- convert ordinal columns to single number-ordered columns
- did not deal with text data (further work: NLP??)

### Label Encoding
- originally only %female>50% count as female-led
- wanted to add "co-led" and turn it to multi-class but too complicated because many imbalanced data algorithms are targeted for binary class but definitely are worth exploring

### Dealing with Imbalanced Dataset

4. K-means clustering --> `kmeans_v1`
- the idea is to cluster exclusively on the majority class and to break it down to several equal-sized small groups
- however, the problem with k-means clustering was that no matter how many clusters I made, the classification was still extremely imbalanced, with a majority class of 2570/2858 even when k=10
- make sure to scale the data before fitting it in the model!

5. K-modes clustering --> `kmodes`
- kmodes clustering is an alternative from kmeans, for categorical data
- another advantage of kmodes is that it creates equal-sized cluster groups

check other clustering methods: https://scikit-learn.org/stable/modules/clustering.html
- see if there is stability in the clusters

x. Resampling: Random Over-sampling / Under-sampling --> [notebook_name]

-  Over-sampling: Instead of creating exact copies of the minority class records, we can introduce small variations into those copies, creating more diverse synthetic samples.

- Under-sampling: We can cluster the records of the majority class, and do the under-sampling by removing records from each cluster, thus seeking to preserve information

### Dealing with Too Many Features: Dimensionality Reduction

x. Principal Component Analysis (PCA)
- pca --> set variance threshold and get columns and feed back into xgboost
- at the same time look at top features selected by xgboost and compare results

## Classification

x. xgboost_v1: no hyper parameter tuning, no dealing with imbalanced data

model_version | feature selection | imbalanced class | hyperparameter tuning | cross validation
--------------|-------------------|------------------|-----------------------|-----------------
xgboost_v1 | no | no | no | no
xgboost_v2 | yes, top100 | no | no | no
xgboost_v3 | yes, top all 1352 | no | no
xgboost_v4 | yes, top all 2xxx | yes | no | no


Backlog
- [techniques to deal with imbalanced data](https://www.analyticsvidhya.com/blog/2020/07/10-techniques-to-deal-with-class-imbalance-in-machine-learning/)
- [other algorithms to try out as baselines and improvements](https://machinelearningmastery.com/framework-for-imbalanced-classification-projects/)
