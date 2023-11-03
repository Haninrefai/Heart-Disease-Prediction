# Heart Disease Classification With Stratified K-Fold Cross Validation Sampling
  
#### Abstract—Cardiovascular diseases (CVDs) are the leading cause of death globally [1]. An estimated 17.9 million people died from CVDs in 2019, representing 32% of all global deaths [1]. Of these deaths, 85% were due to heart attack and stroke, highlighting the urgent need for accurate and efficient heart disease prediction [1]. Machine learning techniques have emerged as a promising solution for addressing this challenge, offering high accuracy and sensitivity in heart disease classification. In this paper, I present a comprehensive review of multiple machine learning methods for heart disease classification, including decision trees and support vector machines. I also examine the various features used for heart disease classification, such as medical history and clinical measurements. Furthermore, I highlight the challenges and limitations of existing methods and provide suggestions for future research in this area. Overall, this review underscores the significance of machine learning in achieving accurate and reliable heart disease classification with high sensitivity, ensuring that all individuals with the disease are correctly identified, which is essential for improving patient outcomes.

#### Keywords— heart disease, cardiovascular disease, features, attributes, machine learning classification, Stratified K-fold Cross Validation, Support Vector Machine (SVM), Decision Tree (DT), GridSearchCV, sensitivity, accuracy, overfitting

### Introduction
Heart disease is a major public health concern worldwide, causing significant morbidity and mortality. It is a leading cause of death globally and accounts for a significant proportion of healthcare expenditure. Early and accurate diagnosis of heart disease is essential for improving patient outcomes, reducing healthcare costs, and mitigating the global burden of cardiovascular disease. Machine learning has emerged as a promising solution for improving heart disease classification and prediction. The use of machine learning algorithms in heart disease classification can provide high accuracy and sensitivity, enabling early detection and intervention for patients with the disease. Moreover, machine learning can help to identify previously unrecognized risk factors and improve understanding of the underlying mechanisms of heart disease. Therefore, studying heart disease classification using machine learning is important as it can lead to the development of more accurate and efficient diagnostic tools. Furthermore, it can contribute to a better understanding of the disease and its risk factors, which can inform the development of effective preventive strategies.


### Theory
In the dataset, the target class, ‘HeartDisease’ is a binary class. In this case, the proposed analytics solution is applying classification machine learning models such as Support Vector Machine Classifier (SVM) and Decision Tree Classifier (DT). SVM finds a hyperplane that maximally separates the different classes in the dataset. On the other hand, DTs can identify the most informative features for predicting heart disease where they can be also utilized for feature selection. Moreover, DTs are easy to understand and interpret since they provide a transparent model that can be easily explained to clinicians and patients. One key feature in both proposed models, that they are robust to outliers in the data, and they can handle noisy datasets especially the case of classifying heart disease since outliers are expected in some of the measures used to predict the disease. SVM only considers the data points that are closest to the decision boundary, which makes it less sensitive to outliers and noise, while DT focuses on the most informative features based on a specific measure of randomness in data features.

### Methods
#### Data explanation and characterization
I obtained the dataset from Kaggle, and it was originally created using a combination of preexisting data from different cities and countries. The dataset was filtered to remove duplicate entries resulting in the final data having 918 instances, 11 descriptive features, and 1 target feature [2]. There are seven categorical features, six are continuous features, and one is the target variable.  
 
##### TABLE I. DATA QUALITY REPORT FOR CATEGORICAL FEATURES
 ![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/7721597d-cc2a-47fe-8e8f-41976f4255d1)

Sex represents the gender of the patient. This feature takes F or M values, F for female and M for male, making the cardinality of this feature two. The mode of the Sex feature is M with a frequency of 725 which means that males occupy around 79% of the dataset. 
ChestPainType feature gives the type of chest pain, which can be TA meaning Typical Angina, ATA meaning Atypical Angina, NAP meaning Non-Anginal Pain, or ASY meaning Asymptomatic. Angina is defined as a “type of chest pain caused by reduced blood flow to the heart” [3]. Typical angina is usually preceded by physical exertion or stress and is relieved with rest or medication. Atypical angina is described as having symptoms that are ascribed to angina but don’t fall under the category of typical angina [4]. Non-Anginal Pain refers to pain in the chest area that is not related to the heart [5]. Asymptomatic is when there are no symptoms being shown. Thus, ChestPainType has a cardinality of four since its domain is TA, ATA, NAP, and ASY. ASY chest pain type is the most frequent value, where 54% of the patients have asymptomatic chest pain. This signifies the importance of performing statistical data analysis on the dataset.
Fasting BS is fasting blood sugar which is your blood sugar level after an overnight period of no eating [6]. FastingBS is a Boolean with a domain of 0 or 1, so its cardinality is two. It has a value of 1 if the fasting blood sugar is greater than 120 mg/dl and 0 otherwise. Zero is the mode of this feature with 77% of the instances having fasting blood sugar levels that are less than or equal to 120 mg/dl. 
Resting ECG is resting electrocardiogram results which can be Normal, LVH, or ST. Resting ECG is a test that can help detect heart abnormalities like arrhythmia and show evidence of heart disease and left ventricular hypertrophy (LVH) [7]. ST refers to ST-T wave abnormality which is when there is an elevation or depression of the region between the ventricular end of depolarization and the beginning of repolarization and/or T wave inversions [8]. This can be indicative of myocardial ischemia or myocardial injury which are conditions related to the heart [8]. Resting ECG measured in millivolts (mV). Resting ECG has a domain of Normal, ST, and LVH making the cardinality three. The mode of this feature is Normal, as patients with Normal ECG results make up 60% of the instances. 
ExerciseAngina refers to whether angina was induced by exercise or not. ExerciseAngina has a cardinality of two since its domain is Yes or No. The mode of this feature is No. About 60% of the Angina cases were not induced by exercise.
ST_Slope is the ST segment's slope which measures the segment's shift “relative to exercise-induced increments in heart rate” [9]. It can be up-sloping, flat, or down-sloping. Therefore, the feature has a cardinality of three: up, flat, and down. Half of the dataset had a flat slope during peak exercise. 
Finally, the target feature is titled ‘HeartDisease’ and is a Boolean with a domain of 1 and 0, 1 being the patient has heart disease, and 0 being the patient does not have heart disease. HeartDisease has a cardinality of two, with 44.6% of the patients have heart disease. This indicates that there is a balanced distribution between patients who have been diagnosed with the disease and those who have not, thereby ensuring a representative sample for the study.

##### TABLE II. DATA QUALITY REPORT FOR CONTINUOUS FEATURES
![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/664246ee-44d2-4087-ab1f-750ff4ff98b4)
 

Age represents the age of the patients, and its values range from 28 to 77, with a mean of 53.5.
Resting BP, measured by millimeters (mm) of mercury (Hg), stands for resting blood pressure which is the blood pressure when your heart is at rest. Resting BP attribute has a domain of 0 to 200. The values signify the presence of outliers, since a zero-blood pressure means a dead person and 200 is an extreme blood pressure value. 
Cholesterol gives the serum cholesterol level which is the amount of total cholesterol in your blood [10]. It is measured by milligrams (mg) of cholesterol per deciliter (dL) of blood (mm/dl).  Cholesterol attribute has a domain of 0 to 603. The zero values and the high range indicate the presence of outliers, as no human can have a zero-cholesterol level. This value could have been inputted as zero to fill in untested cholesterol levels for some patients. Additionally, the standard deviation for cholesterol levels is 109.4 which is very high. 
MaxHR is the maximum heart rate achieved. It ranges between 60 and 202 with a mean of 136.8 and a standard deviation of 25.5. A heart rate of 202 beats per minute is very high and falls into the category of tachycardia, which is a rapid heart rate. 
Finally, oldpeak is the measure of ST depression induced by exercise relative to rest. It is measured based on levels of depression. Oldpeak has a minimum of -2.6 and a maximum of 6.2 with a 1.07 standard deviation.  

#### Data Visualization

##### Fig. 1. Bar Plots of Categorical Features
![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/70142f28-369d-4d76-be3a-96e02032ba99)

As shown in fig. 1, the bar plot for the Sex feature shows that the number of males is almost four times the number of females in the dataset. The ASY (Asymptomatic) chest pain type is the most prevalent type of chest pain at almost 400 instances, while TA (Typical Angina) scores the lowest at a level lower than 100. The number of instances where fasting blood pressure is less than or equal to 120 mg/dl is 3.5 times more than the number of instances where fasting blood pressure is greater than 120 mg/dl. Additionally, the number of instances with Normal resting ECG is larger than the number of instances of LVH, which shows probable or definite left ventricular hypertrophy by Estes’ criteria, and ST which shows the patient is having wave abnormality with elevation or depression of more than 0.05 mV. This means that there might be people with heart disease that have normal resting ECG. As for ExerciseAngina, the number of cases with ‘No’ Exercise Angina is around 375, which is higher than the number of cases of Exercise Angina. Instances with flat ST_Slope, zero slope, are the largest number of instances compared to upward or downward slopes. Finally, the number of instances of heart disease is slightly higher than instances of no heart disease with a difference of 100 instances.
 
##### Fig. 2. Histograms of Continuous Features
![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/f300b30a-6a5d-4dea-8cc8-2cf17cc0c361)

In fig. 2, the histogram of the Age feature shows a unimodal normal distribution. On the other hand, RestingBP follows a unimodal right-skewed distribution, which will require normalization before applying any machine learning model. Also, 350 instances fall around 125 mm/Hg RestingBP. As for the Cholesterol feature, there are 175 instances with 0 to 50 mm/dl cholesterol levels which shows the presence of outliers in the feature. The rest of the data has a right-skewed unimodal distribution with up to 600 mm/dl cholesterol levels, reflecting large outlier values. For the MaxHR feature, it follows a multimodal distribution with two peaks at 120 and 140, with 120 instances at each peak. The Oldpeak feature follows a unimodal right-skewed distribution with the highest concentration being at 0.

#### Data preprocessing
As the data quality report shows for both types of attributes, there are no missing values nor duplicates in the dataset. However, I encoded the categorical features in the dataset. I label encoded Sex and ExerciseAngina making M and Y as 0 and F and N as 1, respectively. I hot encoded the rest of the categorical features such as ChestPainType, Resting ECG, ST_Slope since each of the features has multiple levels. Additionally, I scaled the data between zero and one to put all the continuous features in the same range to equalize the influence of the features. I used the min-max scaler since I am applying SelectKBest with Chi2 feature selection method in the following steps, and this method only accepts non-negative values. After encoding, I ended up with 19 attributes.
a_i^'=  (a_i-min⁡(a))/(max⁡(a)-min⁡(a))×(high-low)+low

In this study, I explored the impact of outliers on heart disease classification by applying machine learning models on both outlier-removed and outlier-included datasets. To remove outliers, I used the Interquartile Range (IQR) method, which involves clamping the outliers in the continuous data features. Specifically, any data point less than (Q1 – 1.5IQR) was set to the value (Q1 – 1.5IQR), while any data point above (Q3 + 1.5IQR) was set to that threshold value. It should be noted that outliers are commonly observed in clinical tests of heart disease patients, where some test values may deviate significantly from the normal range.
I conducted a visualization of the data to identify features that have the strongest correlation with the target feature. While it is important to note that correlation does not necessarily imply causation, the strength of the correlation can provide an indication of how changes in those features may be linked to changes in the target feature. However, even after reducing the correlation threshold values to between [-0.5, 0.5], the resulting correlation values between the features and the target feature were not indicative of strong correlation. Only three features, namely St_Slope_Up, ST_Slope_Flat, and ChestPaintType_ASY, exhibited a correlation with HeartDisease that surpassed the threshold. Therefore, I utilized feature selection methods to reduce the number of features in the dataset, as the majority of features were not strongly correlated with the target feature.

 

![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/b5978bfc-e2f6-4f6d-aefe-d231af517846)
Fig. 3. Correlation with Target Class

I split the dataset into training and testing, with a training set size of 80% and test set size 20%. To ensure that all implemented models would always produce the same results. Throughout any data splits, I set the random_state parameter to a fixed integer value of 42 to fix the random seed for the random number generator. This ensures that the results of the models are reproducible and consistent across multiple runs. I used the training set to apply feature selection methods. Using k-fold cross validation with 5 folds, I applied a backward selection method Recursive Feature Elimination (RFE) with a decision tree estimator. Based on the RFE rankings, the top 10 features are ST_Slope_Up, Cholesterol, MaxHR, Age, Oldpeak, ChestPainType_ASY, RestingBP, Sex, ExerciseAngina, and FastingBS. To verify the results of RFE, I implemented another feature selection method called SelectKBest with Chi squared. This method is a filter method that selects the top K features based on the Chi-squared test statistic between each feature and the target variable. With SelectKBest, the top 10 features are Sex, FastingBS, MaxHR, ExerciseAngina, ChestPainType_ASY, ChestPainType_ATA, ChestPainType_NAP, ST_Slope_Down, ST_Slope_Flat, and ST_Slope_Up. The results are consistent between both feature selection methods with some variations. For instance, Cholesterol and Oldpeak were only picked by RFE, while all ST_Slope levels are ranked high in SelectKBest. Therefore, I chose 11 features instead of 10 to create the dataset with the selected features. The selected features are Age, Sex, FastingBS, MaxHR, ExerciseAngina, Oldpeak, ChestPainType_ASY, ChestPainType_ATA, RestingECG_Normal, ST_Slope_Flat, and ST_Slope_Up. 
	
#### Data analysis/mining
I started by creating a new data frame named “df_Ml” based on the selected features from the dataset. To train and evaluate machine learning models, I randomly split the dataset into a training set of 80% and a test set of 20%, with a random state of 42 for consistency. To ensure the reliability and generalizability of my models, I utilized the stratified k-fold method for cross-validation, which ensures equal representation of all classes in each fold. The k-fold cross-validation was applied to the 80% training set, and the model was then re-evaluated on the unseen 20% test set to avoid any data leak. I used two popular models, the Support Vector Machine Classifier (SVM) with a linear kernel and the Decision Tree Classifier (DT), as they are known for their robustness and ability to handle noisy data with outliers. I also tested both models on the non-removed outlier version of the dataset to assess their ability to handle such data. To ensure the robustness of the results, I repeated the model implementation experiments several times. First, I used the df_Ml data frame, then I applied GridSearchCV to the same dataset, and finally, I used the originally encoded dataset. I evaluated both models after each experiment to obtain results that were consistent and reproducible. 

#### Evaluation and interpretations
For both the Support Vector Machine Classifier (SVM) with a linear kernel and the Decision Tree Classifier, I calculated the mean accuracy across the stratified five cross-validation folds and obtained the confusion matrix for each model. Additionally, I visualized the Receiver Operating Characteristic curve (ROC) for each model. ROC is a graphical representation of the performance of a binary classification model. The curve is created by plotting the true positive rate (TPR) against the false positive rate (FPR) at various threshold settings. The area under the ROC curve (AUC) is often used as a metric to evaluate the overall performance of a classifier. A perfect classifier would have an AUC score of 1, while a random classifier would have an AUC score of 0.5. However, since this is a medical case where the model's ability to correctly identify positive cases (sensitivity) is of utmost importance, I placed particular emphasis on calculating model sensitivity for each experiment. Sensitivity is the true positive rate (TPR) measures the percentage of true positive cases out of all positive cases, which is important for medical diagnosis and treatment as false negatives can be potentially harmful to patients. If TPR is high, it means that the model is correctly identifying a large portion of actual positives, and therefore the false negative rate (FNR) will be low, indicating that the model is correctly classifying a smaller portion of actual positives as false negatives.

### Results
#### First experiment using dataset with selected features
With the stratified k-fold cross validation SVM scored a mean of 0.87 accuracy on training set and a mean of 0.87 on validation set, and a sensitivity value of 0.88. Additionally, it scored 0.86 accuracy on the test set, and a sensitivity of 0.88. On the other hand, DT scored a mean of 1.00 on training data and a mean of 1.00 on validation data. In this case, the sensitivity is also 1. This might seem like a prefect model; however, this result is alarming since it is an indication of overfitting. Surely, overfitting is proven by the test accuracy that fell to 0.77 on unseen data. Yet, the sensitivity of the model was 0.84.  

#### Second experiment using dataset with selected features and GridSearch Cross Validation (GridSearchCV)
Grid search is a method used for optimizing the hyperparameters of machine learning models. It involves an exhaustive search over a specified range of parameter values for an estimator, to find the optimal hyperparameters that result in the highest possible accuracy. To implement a grid search, a dictionary with potential parameter values for each model is created and fed into the scikit-learn GridSearchCV method. This technique allows for a systematic evaluation of different hyperparameter combinations, enabling the model to perform at its best on new, unseen data.
For SVM, the optimal hyperparameters are C = 10, class_weight = None, degree = 2, gamma = scale, and kernel = rbf. Setting C to 10 in SVM means that the penalty for misclassification is relatively high, which may result in a smaller margin separating the classes. This is needed because the data is not linearly separable which is evident from the degree parameter that is set to two. Similarly, due the data being non-linearly separable, the rest of the parameters are chosen, where gamma is set to scale to ensure that the kernel coefficient is calculated based on the variance of the data and scales inversely proportional to the number of features. Besides, Radial Basis Function (RBF) is the kernel function set by the grid search. After tuning the hyperparameters or SVM, the test accuracy of the optimized SVM remained at 0.86. Nonetheless, the sensitivity of the optimized SVM increased to 0.9, which is a higher and favorable result compared to the first experiment.
After the alarming results of DT performance, I decided to run the grid search to tun its hyperparameters. The best hyperparameters are entropy for the criterion, 5 is the max_depth, sqrt for max_features, min_samples_leaf = 1, and min_samples_split = 5. After fitting the tuned DT to the test set, both the accuracy improved to 0.85 and sensitivity remained the same at 0.84.  

#### Third experiment using dataset without feature selection
In this experiment, I also used stratified k-fold cross validation with five folds. I implemented SVM with RBF kernel function. It scored a mean of 0.88 on both training and validation sets. The accuracy dropped to 0.85 on unseen test data. SVM’s sensitivity on test data was 0.88, which is a lower result than experiment two. Alternatively, DT also overfitted on training and validation set in this experiment scoring a mean of 1.00 on both. Yet, the results improved on test data compared to experiment one to record a test accuracy of 0.82; however, this value is lower than the second experiment with grid search. Furthermore, sensitivity improved to 0.88 on test data, which is better than both preceding experiments. 

### Results and Performance Analysis

![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/bf7321f4-f35c-4eb6-9fc0-e68eeb7cb069) 
Fig. 4. SVC ROC Curve is based on a test set in the 1st experiment.

In figure 4, the AUC of SVM when run on test data is significantly large, which indicates a good performing model overall. 

![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/42f83fd7-e2d6-4652-8d0c-b9df47a61e13)
Fig. 5. DT ROC Curve is based on a test set in the 1st experiment.

In figure 5, the AUC of DT in the first experiment depicts a perfect model; however, such result is an indication of overfitting. This could be due to using the DT estimator in the initial feature selection step, where the model already picked the most informative features.


![image](https://github.com/Haninrefai/Heart-Disease-Prediction/assets/89818668/6b0a338c-4149-40ba-a31c-de70c7b73a41) 
Fig. 6. SVM ROC Curve is based on a test set in the 3rd experiment.

In figure 6, the AUC of SVM in the third experiment in which there were no feature selection performed on the dataset is 0.94 which is higher than that of feature selected dataset. This may mean that I could have introduced some bias by manually selecting the 11 features of the df_Ml dataset.

### Discussion and Conclusion 
By performing simple statistical analysis of the dataset, 54% of the patients have asymptomatic chest pain, which is indicative of the importance of the feature ChestPainType¬_ASY. Additionally, even though feature selection helps to simplify the models and make them easier to interpret, and have shorter training times, bias can be introduced by setting specific thresholds such as maximum number of features or ranking values. Therefore, I think that applying Prinicpal Component Analysis (PCA) may be a better choice to reduce dimensionality of the data and choose the features that capture the most variance in the dataset. 
As mentioned in the data preprocessing section, I implemented both models on outlier-removed and outlier-included datasets. By comparing the performance of the machine learning models trained on both datasets, I aimed to evaluate the impact of outliers on heart disease classification accuracy. The results were very similar in this case not because outliers do not affect predictions, but it is due to my preference bias in choosing machine learning models that are robust to outliers. This should be considered when applying other classification models. 
It is also significant that higher performance models with higher accuracy and AUC value are not indicative of better models to deploy on unseen real-world data. In this case, I would never deploy DT on this data as it fails to generalize, and it only memorizes. 
Based on the experiments conducted, the optimized SVM model had the highest performance with an optimal sensitivity value of 0.9. Therefore, I recommend deploying this model on the dataset for further use. However, to improve sensitivity further, I suggest experimenting with the optimized SVM model on the dataset with reduced dimensionality after applying PCA and the dataset without any feature selection or reduced dimensionality. This experimentation will help ensure that the model is not overfitting and will allow for a more robust evaluation of model performance.

### References
World Health Organization. World Health Organization. Cardiovascular Diseases (CVDs). https://www.who.int/news-room/fact-sheets/detail/cardiovascular-diseases-(cvds). Accessed April 27, 2023.
Fedesoriano. (September 2021). Heart Failure Prediction Dataset. Retrieved March 15, 2023, from https://www.kaggle.com/fedesoriano/heart-failure-prediction.
Mayo Clinic. (2022, March 30). Angina - Symptoms and Causes. Retrieved April 25, 2023, from https://www.mayoclinic.org/diseases-conditions/angina/symptoms-causes/syc-20369373
AlBadri, A., Leong, D., Bairey Merz, C. N., Wei, J., Handberg, E. M., Shufelt, C. L., Mehta, P. K., Nelson, M. D., Thomson, L. E., Berman, D. S., Shaw, L. J., Cook‐Wiens, G., & Pepine, C. J. (2017). Typical angina is associated with greater coronary endothelial dysfunction but not abnormal vasodilatory reserve. Clinical Cardiology, 40(10), 886–891. Retrieved April 25, 2023, from https://doi.org/10.1002/clc.22740 
CDC. (2019, May 15). Diabetes Testing. Centers for Disease Control and Prevention. Retrieved April 25, 2023, from https://www.cdc.gov/diabetes/basics/getting-tested.html#:~:text=Fasting%20Blood%20Sugar%20Test 
Centre (UK), N. G. (2016). Resting electrocardiography. National Library of Medicine; National Institute for Health and Care Excellence (UK). Retrieved April 25, 2023, from https://www.ncbi.nlm.nih.gov/books/NBK367910/ 
Kashou, A. H., & Kashou, H. E. (2019). Rhythm, ST Segment. StatPearls Publishing. National Library of Medicine. https://www.ncbi.nlm.nih.gov/books/NBK459364/
Non-Cardiac Chest Pain. (n.d.). Cleveland Clinic. Retrieved April 25, 2023, from https://my.clevelandclinic.org/health/diseases/15851-gerd-non-cardiac-chest-pain 
Finkelhor, R. S., Newhouse, K. E., Vrobel, T. R., Miron, S. D., & Bahler, R. C. (1986). The ST segment/heart rate slope as a predictor of coronary artery disease: comparison with quantitative thallium imaging and conventional ST segment criteria. American Heart Journal, 112(2), 296–304. Retrieved April 25, 2023, from https://doi.org/10.1016/0002-8703(86)90265-6
Heart UK. (2022). Understanding your cholesterol test results. Heart UK The Cholesterol Charity. Retrieved April 25, 2023, from https://www.heartuk.org.uk/cholesterol/understanding-your-cholesterol-test-results- 
Scikit Learn Machine Learning in Python. (n.d.). Extra Trees Classifier. Retrieved March 31, 2023, from https://scikit-learn.org/stable/index.html.

 

