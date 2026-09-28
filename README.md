# Comparing Classifiers

## Overview

This project compares four classification models for predicting whether a bank customer will subscribe to a term deposit:

* Logistic Regression
* K-Nearest Neighbors (KNN)
* Decision Tree
* Support Vector Machine (SVM)

The analysis includes exploratory data analysis, preprocessing, model comparison, and hyperparameter tuning using the Bank Marketing dataset.

## Business Objective

The goal is to identify customers who are more likely to subscribe to a term deposit so the bank can prioritize marketing efforts and improve campaign efficiency.

## Key Findings

* The target variable is imbalanced:

  * **88.73%** did not subscribe
  * **11.27%** subscribed
* The original Decision Tree showed overfitting:

  * Training accuracy: **100.00%**
  * Test accuracy: **89.29%**
* Hyperparameter tuning improved the Decision Tree test accuracy to **91.85%** with `max_depth=5`.
* Logistic Regression achieved **91.64%** test accuracy.
* SVM achieved **91.45%** test accuracy.
* KNN achieved **90.94%** test accuracy.
* SVM required substantially more grid-search time (**81.12 seconds**) than the other models.
* `emp.var.rate`, `euribor3m`, and `nr.employed` were highly correlated. Only `emp.var.rate` was retained to reduce redundant information.

## Tuned Model Results

| Model               | Best Parameters        | CV Accuracy | Test Accuracy |         Time |
| ------------------- | ---------------------- | ----------: | ------------: | -----------: |
| Logistic Regression | `C=10`                 |      90.98% |        91.64% |     4.47 sec |
| KNN                 | `n_neighbors=11`       |      90.44% |        90.94% |     4.60 sec |
| Decision Tree       | `max_depth=5`          |      91.20% |    **91.85%** | **1.15 sec** |
| SVM                 | `C=10`, `gamma='auto'` |      91.00% |        91.45% |    81.12 sec |

## Actionable Insights

The models can help the bank prioritize customers who are more likely to subscribe rather than treating all customers equally. Because the target is imbalanced, accuracy alone should not be used to assess the model's ability to identify subscribers.

## Recommendations and Next Steps

* Evaluate **precision, recall, F1 score, and confusion matrices** in addition to accuracy.
* Pay particular attention to the positive `yes` class.
* Investigate class-weighting techniques to improve identification of subscribers.
* Evaluate the models **without `duration`** if predictions need to be made before contacting customers, since call duration is only known after the interaction.
* Validate the selected model on additional or future customer data.

## Conclusion

After tuning, the **Decision Tree achieved the highest test accuracy in this experiment at 91.85%** and reduced the overfitting observed in the original model. Logistic Regression and SVM produced similar accuracy, while SVM required substantially more computation time.

Because the target is imbalanced, final model evaluation should consider precision, recall, F1 score, and the confusion matrix in addition to accuracy.
