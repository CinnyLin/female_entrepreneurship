# Pipeline

## Data Collection

1. Getting raw data from Crunchbase --> [notebook_name]

2. Aggregating data with gender API --> [notebook_name]

## Data Preprocessing

3. Feature engineering --> `feature_eng`
- convert all data to numerical
- convert single and multi-categories rows to one-hot-encoded binary columns
- convert ordinal columns to single number-ordered columns
- did not deal with text data (further work: NLP??)

### Dealing with Imbalanced Dataset

4. K-means clustering --> `kmeans_v1`
- the idea is to cluster exclusively on the majority class and to break it down to several equal-sized small groups
- however, the problem with k-means clustering was that no matter how many clusters I made, the classification was still extremely imbalanced, with a majority class of 2570/2858 even when k=10

5. K-modes clustering --> `kmodes`
- kmodes clustering is an alternative from kmeans, for categorical data
- another advantage of kmodes is that it creates equal-sized cluster groups

x. Upsampling / Downsampling --> [notebook_name]

## Classification

x. xgboost_v1: no hyper parameter tuning, no dealing with imbalanced data
