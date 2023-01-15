# An Interpretable Machine Learning Algorithm for Myocardial Infarction

## Problem Description

Myocardial infarction (MI), also known as heart attack, refers to the death of heart muscle because of lack of oxygen supply. According to statistics, approximately 1.5 million cases of myocardial infarction (MI) occur annually in the United States. The mortality rate of acute myocardial infarction (MI) is 30%. About 50% of the deaths occur before arrival at the hospital and an additional 5-10% of survivors die within the first year after their myocardial infarction (Zafari et al., 2019).

Myocardial Infarction is one of the most challenging and complex problems in healthcare since the progress of the disease differs in patients. Complications can be observed frequently and in the period of acute and subacute, they cause to worsening of the disease and even death. There are many types of complications. The most commons are cardiogenic shock, heart failure, embolism, arrhythmia, ischemia, cardiac rupture, angina pectoris, pericarditis, Dressler’s syndrome, and inflammation. The diversity of complications makes it difficult for a specialist to foresee them.

When I look at the guidelines of MI (Collet, J. P. et al., 2020) (Kristensen, S. D. et al, 2018), there is no detailed explanation about the condition of the patient when complications may occur. For this reason, I want to develop an interpretable machine learning algorithm for predicting complications of myocardial infarction. This implementation can help to prevent complications by taking precautions.

## Data Description

We applied our methods to a publicly available dataset with a size of 1700 patients. The dataset was collected in a clinical hospital in Krasnoyarsk, Russia from 1992-1995. The database contains information about 111 medical features and a binary output representing if a patient with myocardial infarction shows complications or not.

There were several variable categories in the dataset:
- General input values (e.g., ID, age, gender),
- Inputs from anamnesis (e.g., arrhythmia, obesity, bronchial asthma, exertional angina pectoris in the anamnesis),
- Inputs from electrocardiography (e.g., ventricular fibrillation, sinoatrial block on ECG), 
- Inputs from the serum (e.g., serum potassium content, serum sodium content)
- Inputs from intensive care units (e.g., use of liquid nitrates in ICU, use of opioid drugs in the ICU), and
- Results from the emergency cardiology team (e.g., systolic blood pressure, diastolic blood pressure according to the emergency cardiology team).

## Data Preprocessing

### Missing Values

I applied several pre-processing methods to get the dataset ready for further analysis. First, I deleted rows and columns with missing values more than a threshold. I selected the threshold according to common practices of machine learning articles. I deleted rows and columns of which more than 30% of data points are missing. As a result, 7 columns and 24 rows were deleted.

For the remaining rows and columns with missing value proportion less than 30%, I applied data imputation. I applied ‘k-nearest neighbor’ imputation for binary and continuous variables. As the name suggests, the ‘k-nearest neighbor’ imputation strategy looks at nearest neighbors to determine the imputed value. For binary variables, I applied the ‘most frequent’ imputation strategy. This prevented binary values from having fractional values. With the ‘most frequent’ strategy, the missing values in binary variables will only be filled with either 0 or 1. This way, I filled the missing values for the entire dataset.

### Categorical Variables

After imputing missing values, our categorical variables still had the problem of being ordered. Machine learning algorithms cannot directly work with categorical data. The categories are usually ordered. These ordered categories must be converted into numbers. The usual approach is to apply one-hot-encoding. With one-hot-encoding, each categorical level becomes a separate feature in the dataset with binary values (1 or 0). This allows machine learning algorithms to read categorical data in a better way.

### Continuous Variables

Another problem I encountered was that the continuous variables had different scales. This would cause continuous variables with large values to affect the algorithm more. To avoid this problem, I applied centering; I subtracted the mean from each continuous variable and divided them into their standard deviation. This way, each continuous variable had zero mean and one unit of standard deviation.

### Imbalanced Data

Our dataset initially had imbalanced data. some complications were a minority, and some were a majority. Thus, I merged all complications together and binarized the myocardial infarction complications output. I simplified the output of a patient to a binary decision, i.e., whether a patient has a complication or not. With this modification, I ended up with a binary classification problem. If a patient has a myocardial infarction complication, the output is one. Otherwise, it is zero.

## Methodology

In predicting the occurrence of complications, supervised machine learning algorithms are employed. As it is one of the aims of this study to present the decision-makers with insights over what features are important in predicting complications before they occur, only a few sets of machine learning algorithms can be of use for the study. Therefore, in order to render the results more interpretable, tree-based algorithms were put into use. Among the family of treebased algorithms, 3 of the algorithms – namely, simple decision tree, random forests, and XGBoost – were chosen as these algorithms approximately represent the different variety of the tree-based algorithms to a great extent.

As the aim of the study is to have interpretable results, I used the recursive feature elimination technique in the training set where the number of features that produces the best accuracy – the percentage of observations predicted correctly – results were identified for each decision tree and random forest algorithms. Once these number of features are found, I also identified the actual features that fall under these set of features for each algorithm. Finding these set of features for each algorithm, in turn, allowed to build the actual algorithms based on these features, instead of using all of the features in the dataset that would have been more likely to produce less interpretable results. Consequently, I narrowed down the features for simple decision tree to 15 features, and 20 features in random forest.

For XGBoost algorithm, a different approach was used in identifying the most relevant features. Instead of using recursive elimination, feature importance2 of the XGBoost algorithm was generated to see which of the features are the most critical in the prediction of complications. Informed by the feature importance graph, I identify the most relevant features to be used in the algorithm. In the end, for the simple decision tree and XGBoost there were 3 different feature sets with different feature numbers are identified to build the models, whereas for random forest set of features used was 4.

