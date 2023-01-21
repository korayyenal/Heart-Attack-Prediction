# Myocardial Infarction Prediction using Interpretable Tree-Based Methods

## Problem Description

In this project, I build and compare interpretable tree-based methods for predicting complications of myocardial infarction (i.e., heart attack).

The main goal is to present decision-makers some insights over what features are critical in predicting complications before they occur.

The task is to predict whether the patient will incur a complication or not (a binary classification problem) given the patient's characteristics.

I apply methods to a publicly available UCI dataset with a size of 1700 patients. The dataset was collected in a clinical hospital in Krasnoyarsk, Russia from 1992-1995. The database contains information about 111 medical features and a binary output representing if a patient with myocardial infarction shows complications or not.

## Data Description

I applied the methods to a publicly available dataset with a size of 1700 patients. The dataset was collected in a clinical hospital in Krasnoyarsk, Russia from 1992-1995. The database contains information about 111 medical features and a binary output representing if a patient with myocardial infarction shows complications or not.

There were several variable categories in the dataset:
- General input values (e.g., ID, age, gender),
- Inputs from anamnesis (e.g., arrhythmia, obesity, bronchial asthma, exertional angina pectoris in the anamnesis),
- Inputs from electrocardiography (e.g., ventricular fibrillation, sinoatrial block on ECG), 
- Inputs from the serum (e.g., serum potassium content, serum sodium content)
- Inputs from intensive care units (e.g., use of liquid nitrates in ICU, use of opioid drugs in the ICU), and
- Results from the emergency cardiology team (e.g., systolic blood pressure, diastolic blood pressure according to the emergency cardiology team).

## Data Preprocessing

I apply the following pre-processing techniques:

- Removing columns/rows with too many missing values
- K-nearest neighbor imputation (binary and continuous variables)
- Most-frequent imputation (categorical variables)
- One-hot encoding (categorical variables)
- Standardization (continuous variables)

## Methodology

Remember that the goal of this study is to present decision-makers insights over what features are important in predicting complications before they occur. Consequently, only a few sets of machine learning algorithms can be of useful, as most machine learning algorithms are not interpretable.

With this goal in mind, I use the following tree-based methods:

- Decision Tree
- Random forest
- XGboost

, where these algorithms pretty much represent the variety of tree-based algorithms to a great extent.

### Recursive feature elimination 

I use Recursive Feature Elimination technique to identify the number of features with the best accuracy for both decision tree and random forest algorithms.

Once I find the number of features, I identify the selected features for each algorithm.

Finding the selected features for each algorithm allows to build the actual algorithms based on these features, instead of using all the features in the dataset, which would have been more costly and likely to produce less interpretable results

For XGBoost algorithm, a different approach was used in identifying the most relevant features. Instead of using recursive elimination, feature importance2 of the XGBoost algorithm was generated to see which of the features are the most critical in the prediction of complications. Informed by the feature importance graph, I identify the most relevant features to be used in the algorithm. In the end, for the simple decision tree and XGBoost there were 3 different feature sets with different feature numbers are identified to build the models, whereas for random forest set of features used was 4.

## Results

### Most important features

When I compare the results of the feature selection for each algorithm, 9 most important features are the same. These features are the following:

- Age
- Serum potassium content (K_BLOOD)
- Serum sodium content (Na_BLOOD)
- Serum A1AT content (ALT_BLOOD)
- Serum AsAT content (AST BLOOD)
- Erythrocyte sedimentation rate (ROE)
- White blood cell count (L_BLOOD) 
- Systolic blood pressure according to intensive care unit (S_AD_ORIT)
- Diastolic blood pressure according to intensive care unit (D_AD_ORIT)

### Accuracy

The results of each model can be found in Table 5.1, where various indicators showing the performance of each model are tabulated.4 The models with the highest accuracy scores for each algorithm are highlighted. As can be observed, it is the random forest algorithm with 20 features that gives the best accuracy results.

### ROC Curves

A similar performance result can be found in Figure 5.1 where Receiver Operating Curve (ROC) and Area under the Receiver Operating Curve (AUC) for each of these models are shown in which the horizontal axis represents the false positive rates and the vertical true positive rates. Indicating the probability with which the algorithm can predict any observation correctly, a higher AUC score shows that the algorithm is more capable of distinguishing between the complications and no-complications. With 0.5 AUC score signifying an algorithm having a 50% chance of distinguishing between classes, it was found that XGboost with all of the features have 0.72 AUC, while random forest with 20 features has 0.70 AUC, followed by 0.65 AUC of simple decision tree with 15 features.

## Limitations and Future Directions

My study had several limitations. 

First, there were many missing values in the data. Thus, I had to delete the records of many patients. This may lead to a sampling bias. The solution is to collect more samples that are complete. 

Second, I also had to remove features with missing values above a certain threshold. I do not know if those features were significant; I had to remove them, nonetheless. If they were significant, those features might have increased the accuracy of the data. Thus, as the next step, I could incorporate more features that are either deleted. The number of features would increase complexity, but I can always reduce the number by applying a dimensionality reduction algorithm such as Principal Component Analysis (PCA).

Third, I obtained low accuracy from the machine learning algorithms (around 65%). The accuracy results are a little better than a random choice. This low accuracy may be the result of several reasons. One reason might be that the algorithms were not good enough, because they were linear. As a solution, I could use more complex/non-linear algorithms, such as Deep Neural Networks that can increase accuracy at the expense of interpretability. Another possibility is that I had a limited number of data, only 1700 instances. In machine learning, this number is usually not sufficient for algorithms to converge to good accuracy. Thus, I may increase the number of training data that leads algorithms to learn better. Yet another reason might be that the features included in the model simply cannot account well enough for myocardial infarction complication. As a solution, I may get more data using a completely new set of features.
