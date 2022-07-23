# Stroke Prediction

This is For [InClass Prediction dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset)

---

## description 
- the goal was to predict predict  whether a patient is likely to get stroke based on the input parameters.
- According to the World Health Organization (WHO) stroke is the 2nd leading cause of death globally, responsible for approximately 11% of total deaths. 
- Each row in the data provides relavant information about the patient.
- ---


## File descriptions
- synth_dataset.csv - the training-testing set.

---

## Data fields
* ID - an ID for this instance
* gender- "Male", "Female" or "Other".
* age- age of the patient .
* hypertension- 0 if the patient doesn't have hypertension, 1 if the patient has hypertension.
* heart_disease- 0 if the patient doesn't have any heart diseases, 1 if the patient has a heart disease.
* ever_married- "No" or "Yes".
* work_type- "children", "Govt_jov", "Never_worked", "Private" or "Self-employed".
* Residence_type- "Rural" or "Urban".
* avg_glucose_level- average glucose level in blood.
* bmi- body mass index.
* smoking_status- "formerly smoked", "never smoked", "smokes" or "Unknown"*.
* stroke- 1 if the patient had a stroke or 0 if not.



---


## Technologies and algorithms used

### algorithms

* Support Vector Machine Classifier(Deprecated)
* Random Forest (Deprecated)
* XGBoostClassifier (Used)
### technologies

* Bagging
* Boosting
### Feature Engineering and Preprocessing 

* A) stroke to non-stroke ratio is very low only 4% had strokes so the data is imbalanced
	* for solving imbalance problem SMOTE may be used (Note: tree-based algorithms doesn't improve by SMOTE as they don't get effected by imbalance problem)
	* I used SMOTE (over sampling technique) as the data is relatively small so if I would use under sampling technique data loss will be a real problem
* B) the data was found Non-nulls except bmi column.
	* nulls in BMI column were filled with means as the missing data is 3% of the data so filling it won't change the data distributio
* C) in Smoking_status Unknown count is very high if we changed it to any other class, it will change the data distribution
  * Smoking_status Unknown represents 30% of the data so I can't drop data with unknown smoking status & it will be considered a status
* D) Used min-max normalization was for two reasons
	* it is not a good Idea to apply standard scaler normalization on non-normally distributed data because it may not give reliable results
	* using standard scaler may not be very reliable on this data as it changes the distribution to be around zero and the data provided can't be negative (wouldn't be so logical)
  
### insights from the graphs: -
* A) higher stroke rates are at older ages which is logic
* B) numerical data isn't normally distributed and their value ranges vary so I'll use min-max scaling
* C) Categorical data is imbalanced
 
 
 
 
### Training The Model

Trained using  CPU


---

## final Score 

* XGBoostClassifier Boost f1_score Train:  0.99
* XGBoostClassifierBoost f1_score test:  0.96

## noted while using the models:
SVM:
	* SVM didn't work well because the normalization technique used before (Min-Max) as it (Min-Max) is affected by outliers but without the normalization accuracy would be worse than this
Decision tree (RF & XGB):
	*Imbalanced data doesn't affect decision trees but as the data is relatively small so I would keep using SMOTE to prevent the models from overfitting (to get real good accuracy as the accuracy of the f1-score may get very high as most of the data would be predicted as false while we care more about true values so that is why I would keep the oversampling)
	*as decision trees don't get affected by normalization (scaling) so using it will not make much difference so I just ignored it
	Random Forest:
		* the Hyper parameters I used are I guess the most effective increasing n_estimators will increase the accuracy slightly but would take more time consuming the computing power
	XGBoost:
		* using these hyper parameters, I got good accuracy with the least overfitting as XGBoost tend to overfit and the data size isn't very large

