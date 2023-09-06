# python_kaggle_heart_disease_prediction
Runs on the dataset in Kaggle at https://www.kaggle.com/datasets/athirags/heart-disease-dataset

Data Check and Evaluate Three Classifier/Prediction Models
Feature Engineering was attempted. The original conclusion remains, the Random Forest Classifier and raw data results below.
Please see the section titled "## Let's do some feature engineering." Mutual Information (MI) scores were taken, auc-roc calculated, and experiments with Logistic Regression (for its speed) to show several attempts at engineering a new feature or two. In the end, none improved the score and only added complexity with often reducing the score. The auc-roc remains in relative agreement with experiments. If a predictor were to be built and have trials run then I'd add more data features and likely use a voting classifier with the three classifiers herein.

I did change out KMeans for K Nearest Neighbors.

Of the models tested, the Random Forest Classifier (RFC) appears to be the best choice with 95% confidence. Logistic Regression and KMeans have means with no statistically significant difference at 95% confidence. There is a small advantage, H0 is rejected based upon none-overlapping confidence intervals at 95% confidence, to using RFC over Logistic Regression or K Nearest Neighbors. The data's ability to provide insights is likely limiting the confidence interval for an average accuracy to (0.6024, 0.6189). This assumes the data was randomly taken, and proves to be unbaised, from the population to which prediction will be applied.

An attempt is made to identify a statistical average mean and confidence interval at 95% confidence for three algorithms to predict heart disease given the sample data provided. The data is also described and explored, and a copy of the results is shared here for each algorithm’s probable mean accuracy and confidence interval.

Two hundred trials were run to determine each confidence interval using 200 unique test and training sample preparations. The idea is that if you train on the whole sample, we would hope new data accuracy averages to the shown mean within its 95% confidence interval. I make no claims here, I am only brushing up on my skills with the best intention of using correct and appropriate methods.

* Logistic Regression Run ** Age and Colestrol prediction with 95% Confidence Interval mean accuracy (0.5916) standard deviation (0.06646568212139875) total bootstraps (200) 95.0% confidence interval for this Logistic Regression model's accuracy: (0.5824, 0.6008)

* KNN Run ** Age, BP, and Cholestrol prediction with 95% Confidence Interval mean accuracy (0.5635) standard deviation (0.04571899318060886) total bootstraps (200) 95.0% confidence interval for this KNN model's accuracy: (0.5572, 0.5699)

* RFC Run ** Agenand Colestrol prediction with 95% Confidence Interval mean accuracy (0.6106) standard deviation (0.05973298783244436) total bootstraps (200) 95.0% confidence interval for this RFC model's accuracy: (0.6024, 0.6189)

The Random Forest Classifier using only Age and Cholesterol data has the highest mean, the highest confidence interval, and its confidence interval does not overlap with those of the Logistic near Regression or KMeans models. With more data it might be possible to have two training sets, a first one taken to test the results of training on the rest of the test data by having the test data split again into a training set and test set. For now, I'm relying on the auc-roc and similar score to give a good double check on the results from the bootstrap runs.

KNN dropped below the Logistic Regression results, they do not have a confidence intervals that contain each other's means. KMeans was removed to test KNN (find an replace style). KMeans could be used, but we'd have to test its clusters to see which is detecting heart disease as true as KMeans is usually used for unsupervised learning and data analysis.

Each algorithm also includes a case where each of the independent variables is dropped one at a time. This can be used to explore the consequences of what Mutivariate Analysis predicts when observing the condition number being large (2620.) "This might indicate that there are strong multicollinearity or other numerical problems." Multicollineartiy can negatively affect regression models, and this helps to explain at least why Logistic Regression performs better with a subset of presumed, but not really, independent variables. I understand that BP and Cholesterol are consider the two leading risk factors for heart disease. I was expecting this to show up and am wondering if there is an issue with the data as two of the models clearly produce on average better results using just Age and Cholesterol as inputs.

The following two variables can be altered to change the output of the exploratory testing in this notebook. percentOfSampleToTest = 0.2 # Original notebook, and the commented values, use 0.2 glb_rnd_state = 45 # this is used so all single run test code below uses the same random_state and gets the same training and test data.

It would be interesting to see if a CNN can improve upon the RFC's prediction confidence interval for the same alpha of 0.05.

Thank you to the Kaggle team for providing both this Jupyter notebook and to ATHIRA G for the sample data. Ilya Yatsyshin, I copied your template and did benefit from seeing your EDA. What follows is new material.
