# Banking+Marketing Challenge

## objective

The objective of this analysis is to predict whether potential customers of a bank client would purchase one of bank's producsts give some of their characteristics.

## Exploratory Data Analysis (EDA)

These are the steps followed in order to explore data:
1- Data was loaded and head and tail of data were printed to have a sense of how data looks like and was organized.

2- Outcome field (y) was looked at to have a sense of how skew the outcome variable is and if data is highly imbalanced. The outcome proportion is approximately one to seven which is considered not bad. Results maybe further improved by attempts to balance data using SMOTE or adjusting model weights.

3- Data types were looked at to have a sense of data and also double check if some of data were stored in wrong formats and need corrections.

4- Overall data distributions were looked at using descrbe() function to have a sense of data distributions and stats.

5- Duplicate entries were checked to avoide data leakage to train-test sets during modeling stage.

6- Checked to see if there are missing (or NaN) values within data that needs special treatments or imputation.

7- According to documentation, there some missing values within data representedas 'unknown' entries. I decided to impute those missing values using KNN method. Python's imputation functionality is very basic. I prefer to use R's MICE package for more complicated imputation techniques.

8- Visualized different data fields to see distributions and qualitatively examine how each of them might relate to each other.

9- Through visualizations I found that two of the fields (pdays, and poutcome) are irrelevant and could be removed. I also found some potential fields (age, duration, consumer price index, and euribor 3 month rate) very relevant for the analysis.


## Data and Predictive Modeling

Following steps were taken to prepare data for the modeling stage:

1- After missing values were imputed using KNN method and also irrelevant fields were removed from data, categorical fields were expanded using one-hot encoding method.

2- Individual values for each categorical fields were examined to ensure they have proper variation for the given field and also see if there are benefits to combine some of the values to reduce uneccessary sparcity and increse variation for each field.

3- Co-linearity among individual fields were looked at to ensure fields are not highly inter-connected to each other.

4- Data were randomly divided into train and test sets. Train set was used to tune and train models and test set was served as independant validation set to check generalization performance of best model.

5- Both train and test sets were normalized. 

6- Different varieties of mL models were examined using the pyCaret package and found that Gradient Boosting classifier has the best performance followed by lightGBM and Random Forest which are all tree-based techniques. This is kind of expected given data is sparse.

7- Calibration curve was plotted to confirm predictive power is appropriate and label imbalance has not much effect on predictive power of the model.

8- Shaply method was used to look at feature importance of all fields uising the best performing model.

9- Neural networks wa snot among methods implemented in pyCaret package. Sp i have implemented a basic network acrchetecture using Keras package. The model was trained on the same training set and was validated on the same test set as those of other ML methods.

## ML Pipeline

Here is a diagram summerizing ML modeling pipeline:


## Model Deployment
