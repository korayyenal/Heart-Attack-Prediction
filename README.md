# An Interpretable Machine Learning Algorithm for Myocardial Infarction

## Problem Description

Myocardial infarction (MI), also known as heart attack, refers to the death of heart muscle because of lack of oxygen supply. According to statistics, approximately 1.5 million cases of myocardial infarction (MI) occur annually in the United States. The mortality rate of acute myocardial infarction (MI) is 30%. About 50% of the deaths occur before arrival at the hospital and an additional 5-10% of survivors die within the first year after their myocardial infarction (Zafari et al., 2019).

Myocardial Infarction is one of the most challenging and complex problems in healthcare since the progress of the disease differs in patients. Complications can be observed frequently and in the period of acute and subacute, they cause to worsening of the disease and even death. There are many types of complications. The most commons are cardiogenic shock, heart failure, embolism, arrhythmia, ischemia, cardiac rupture, angina pectoris, pericarditis, Dressler’s syndrome, and inflammation. The diversity of complications makes it difficult for a specialist to foresee them.

When I look at the guidelines of MI (Collet, J. P. et al., 2020) (Kristensen, S. D. et al, 2018), there is no detailed explanation about the condition of the patient when complications may occur. For this reason, we want to develop an interpretable machine learning algorithm for predicting complications of myocardial infarction. This implementation can help to prevent complications by taking precautions.

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

We applied several pre-processing methods to get the dataset ready for further analysis. First, we deleted rows and columns with missing values more than a threshold. We selected the threshold according to common practices of machine learning articles. We deleted rows and columns of which more than 30% of data points are missing. As a result, 7 columns and 24 rows were deleted.

For the remaining rows and columns with missing value proportion less than 30%, we applied data imputation. We applied ‘k-nearest neighbor’ imputation for binary and continuous variables. As the name suggests, the ‘k-nearest neighbor’ imputation strategy looks at nearest neighbors to determine the imputed value. For binary variables, we applied the ‘most frequent’ imputation strategy. This prevented binary values from having fractional values. With the ‘most frequent’ strategy, the missing values in binary variables will only be filled with either 0 or 1. This way, we filled the missing values for the entire dataset.

After imputing missing values, our categorical variables still had the problem of being ordered. Machine learning algorithms cannot directly work with categorical data. The categories are usually ordered. These ordered categories must be converted into numbers. The usual approach is to apply one-hot-encoding. With one-hot-encoding, each categorical level becomes a separate feature in the dataset with binary values (1 or 0). This allows machine learning algorithms to read categorical data in a better way.

Another problem we encountered was that the continuous variables had different scales. This would cause continuous variables with large values to affect the algorithm more. To avoid this problem, we applied centering; we subtracted the mean from each continuous variable and divided them into their standard deviation. This way, each continuous variable had zero mean and one unit of standard deviation.

Our dataset initially had imbalanced data. some complications were a minority, and some were a majority. Thus, we merged all complications together and binarized the myocardial infarction complications output. We simplified the output of a patient to a binary decision, i.e., whether a patient has a complication or not. With this modification, we ended up with a binary classification problem. If a patient has a myocardial infarction complication, the output is one. Otherwise, it is zero
