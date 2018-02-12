# What's in a good wine?
To answer this question, I am using a dataset with a collection of descriptive and physicochemical characteristics of more than 6000 different wines along with a 'quality rating'. The quality rating represents the median score from three wine experts from 0-10 where 0 is terrible and 10 is excellent. Please use any method(s) you find appropriate to help us understand what makes a wine ‘good’.

I am using Python for my data analysis. Packages include ```pandas```, ```numpy```, ```scikit-learn```, ```statsmodels```, ```seaborn```, ```pandas-profiling``` (data exploration), ```imbalanced-learn``` (over- and under-sampling), and ```mord``` (ordinal logistic regression).

## Results
According to the champion model, a Random Forest Classifer, the most important features from most to least important were ```fixed_acidity```, ```alcohol```, ```volatile_acidity```, ```free_sulfur_dioxide```, ```sulphates```, ```residual_sugar```, and ```type``` (color of wine). 

![img](/img/RandomForestClassifier_FeatureImportances.png)

The selection of these variables agreed with both ordinal logistic regression and ridge classification models, although the logistic model provided odds ratios as well. 

![img](/img/OrdinalLogisticRegression_OddsRatios.png)

From a univariate perspective, the only variable that correlated directly with the quality score was alcohol. This would suggest that alcohol is a large contributer to a wines quality, although I am very skeptical that this is how the somiliers are rating the wines! After looking around the web, I think there are some other factors that contribute to a somilier's opinion of a wine.

![img](/img/AlcoholDistribution_by_Alcohol_and_Color.png)

Despite the lack of strong individual predictors, the Random Forest Classifier achieved an accuracy of 78% on a test set after cross-validation and combined over- and under-sampling. The model had an average f1-score of 0.79.

![img](/img/RandomForestClassifier_ClassificationReport.png)


## Methodology
For this problem, I started by binning the qualities into less granular intervals with 3-4 as the lowest, 5-6 in the middle, and 7-9 as the highest. After consolidating the qualities, I oversampled the outside groups because they had very low sample sizes, and my models before random sampling were basically ignoring them. In conjunction with oversampling the low frequency classes, I undersampled the high frequency classes. After sampling, the models improved drastically and begin predicting the outside classes with better recall.

For models that required standardization (SVM, RidgeRegression), I used a scaling method that's resistant to outliers. All models were cross-validated to tune hyperparamters with either standard scikit-learn methods or more adanaced scikit-learn methods (randomized parameter search).
