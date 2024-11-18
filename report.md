# Alphabet Soup Charity Report

## Overview of the Analysis

### Purpose
Evaluate the performance of the deep learning model created for Alphabet Soup in predicting funding success for applicants.

### Process
The process utilized to analyze this dataset was:
1. Data Preprocessing
  * Reduce Dimensionality: Group infrequent categories into "Other" to reduce the number of dummy variables created. When there are many unique categories, converting each into a separate dummy variable can lead to a very high-dimensional dataset.
  * Convert Data to Numeric Values: Convert categorical data to numeric, and replace SPECIAL_CONSIDERATIONS Y/N values with 0 and 1.
  * Target Variable and Feature Variables: For this analysis the target variable is IS_SUCCESSFUL. This variable indicates whether the funding was used effectively, which aligns with the goal of predicting the success of applicants for funding by the nonprofit foundation Alphabet Soup.

2. Optimization Analysis of Features
  * Pearson Correlation: APPLICATION_TYPE, AFFILIATION, CLASSIFICATION, USE_CASE, and ORGANIZATION all appear to be very influential on the IS_SUCCESSFUL feature.
  * Random Forest: STATUS and the Other columns that were created have very low importance scores, indicating they contribute little to the model's predictiveness.
  * Use Recursive Feature Elimination (RFE) - top 10 Features: ASK_AMT, APPLICATION_TYPE_T10, APPLICATION_TYPE_T19, APPLICATION_TYPE_T3, APPLICATION_TYPE_T4, APPLICATION_TYPE_T5, AFFILIATION_CompanySponsored, AFFILIATION_Independent, CLASSIFICATION_C2000, ORGANIZATION_Association
  * Permutation Importance: Several INCOME_AMT features have negative importance scores, with INCOME_AMT_1-9999 and INCOME_AMT_10M-50M having very low positive importance scores. This indicates that including these features is detrimental to the model's performance, suggesting they may introduce noise rather than useful information.

3. Features Optimization
  * Variables to Remove: An analysis of the features revealed that STATUS and INCOME_AMT have low importane to the model and can be removed. This actually decreased the effectiveness.

4. Compiling, Training, and Evaluating the Model
  * Architecture: The model has four layers - input, two hidden with units of 80 and 30 respectively, and an output layer. Each layer applies batch normalization, a dropout rate of 20%, and utilize the ReLU (Rectified Linear Unit) activation function. 
  * Target Performance: 
  * Steps taken to enhance model performance and their outcomes:
    * Changing the number of units in the first and second hidden layers: This adjustment did not impact the model's accuracy.
    * Adding a batch normalization layer: This standardized the inputs for each mini-batch during training. This adjustment did not impact the model's accuracy.
    * Adjusting the batch size: This adjustment did not impact the model's accuracy.
    * Incorporating a dropout layer: This adjustment did not impact the model's accuracy.
    * Removing features (STATUS and INCOME_AMT): This led to a decrease in the model's accuracy. 
    * Implementing Early Stopping: This led to a decrease in the model's accuracy. 
    * Activation Function: The Exponential Linear Unit (ELU) was tried, but this did not enhance the performance of the model.
    * Adding another hidden layer: This led to a decrease in the model's accuracy. 

5. Performance Analysis
* Precision: The model's predictions are correct 68% of the time, indicating a high number of false positives.
* Recall: The model effectively identifies 88% of actual positive cases, showcasing its strength in capturing positive instances.
* F1 Score: With a score of 0.77, the model reflects a reasonable balance between precision and recall, though there remains room for improvement.
* ROC AUC: A score of 0.79 indicates a decent ability to distinguish between positive and negative classes.
* Confusion Matrix
| Class               | Predicted Negative    | Predicted Positive     |
|---------------------|-----------------------|------------------------|
| Actual Negative (0) | 2184 (True Negatives) | 1853 (False Positives) |
| Actual Positive (1) | 541 (False Negatives) | 3997 (True Positives)  |

6. Summary
The model achieved an accuracy of 73.11%, which is an increase from the baseline original analysis of 72.70%. It demonstrates a strong ability to identify positive cases, as indicated by a high recall, but struggles with precision, leading to a significant number of false positives. Given the context of predicting and analyzing a dataset for a non-profit organization aiming to select applicants for funding with the best chance of success, this model may be acceptable as it helps reduce the risk associated with backing new ventures, which is inherently challenging. Overall, while the model shows promise, particularly in recall, further refinements are necessary to enhance precision and overall effectiveness. Future work may involve exploring additional feature engineering, tuning hyperparameters, or employing alternative modeling techniques to improve performance.