# Banking+Marketing Challenge

## objective

The objective of this analysis is to predict whether potential customers of a client bank would purchase one of bank's products given some of their characteristics.

## Exploratory Data Analysis (EDA)

These are the steps followed to explore data:
1- Data was loaded and head and tail of data were printed to have a sense of how data looks like and how it is organized.

2- Outcome field (y) was looked at to have a sense of how skewed the outcome variable is and if data is highly imbalanced. The outcome proportion is approximately one to seven which is considered not bad. Results maybe further improved by attempts to balance data using SMOTE or adjusting model weights.

3- Data types were looked at to have a sense of data and double checked if some of data were stored in wrong formats and needed corrections.

4- Overall data distributions were looked at using Pandas describe() function to have a sense of data distributions and stats.

5- Duplicate entries were checked to avoid data leakage to train-test sets during modeling stage.

6- Checked to see if there are missing (or NaN) values within data that needed special treatments or imputations.

7- According to documentation, there are some missing values within data represented as 'unknown' entries. I decided to impute those missing values using KNN method. Python's imputation functionality is very basic. I prefer to use R's MICE package for more complicated imputation techniques.

8- Visualized different data fields to see distributions and qualitatively examine how each of them might relate to each other.

9- Through visualizations, I found that two of the fields (pdays, and poutcome) are irrelevant and could be removed. I also found some potential fields (age, duration, consumer price index, and euribor 3 month rate) very relevant for the analysis.


## Data and Predictive Modeling

Following steps were taken to prepare data for the modeling stage:

1- After missing values were imputed using KNN method and irrelevant fields were removed from data, categorical fields were expanded using one-hot encoding method.

2- Individual values for each categorical fields were examined to ensure they have proper variation for the given field and also see if there are benefits to combine some of the values to reduce unnecessary sparcity to the data and/or increase variation for each field.

3- Correlation among individual fields were looked at to ensure fields are not highly inter-connected to each other.

4- Data were randomly divided into train and test sets. Train set was used to tune and train models and test set was served as independent validation set to check generalization performance of the best model.

5- Both train and test sets were normalized. 

6- Different varieties of ML models were examined using the PyCaret package and found that Gradient Boosting classifier has the best performance followed by lightGBM and Random Forest which are all tree-based techniques. This is kind of expected given data is sparse.

7- Calibration curve was plotted to confirm predictive power is appropriate and label imbalance did not affect model's predictive power.

8- Shaply method was used to look at feature importance of all fields using the best performing model.

9- Neural networks was not among methods implemented in PyCaret package. A basic network architecture was implemented using Keras package. The model was trained on the same training set and was validated on the same test set as those of other ML methods.

10- Note for ML model parameter tuning: For this exercise no complicated tuning was implemented however, the best practice is to identify best performing ML model using PyCaret and implement it separately with proper parameter tunings and cross-validation techniques. In practice, I prefer to use Bayesian optimization for better parameter space search.

## ML Pipeline

Here is a diagram summarizing ML modeling pipeline:
![alt text](https://github.com/mpeikari/BankingChallenge/blob/main/ML%20Pipeline.png)


## Model Deployment

A virtual environment sould be created on any of the cloud platforms (AWS, Azure, etc) and all necessary python packages should be installed. The ML model can be trained from scratch on the cloud space or can be uploaded to the cloud.

A user interface should be created that can capture all incoming new data and form data vectors (individually or in batches) in the same way that the model was developed. 

ML predictions can be done as data come in (either through the interface or through other micro-services) in real time or in batches. New data should be stored on the cloud for future model training/maintenance and also debugging purposes. This will allow us to examine possible false positives and false negatives and adjust model if necessary. Prediction logs should also be stored as well to facilitate model debugging.

In order to maintain the model as time passes, there should be other micro-services that can run to automatically re-train the model regularly (if certain threshold of prediction errors reached) or periodically (as the scope of data changes).
