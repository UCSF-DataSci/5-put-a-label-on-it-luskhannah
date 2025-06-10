# Assignment 5: Health Data Classification Results

This file contains your manual interpretations and analysis of the model results from the different parts of the assignment.

## Part 1: Logistic Regression on Imbalanced Data

### Interpretation of Results

In this section, provide your interpretation of the Logistic Regression model's performance on the imbalanced dataset. Consider:

- Which metric performed best and why?
- Which metric performed worst and why?
- How much did the class imbalance affect the results?
- What does the confusion matrix tell you about the model's predictions?

The logistic regression model trained on the imbalanced dataset achieved a high accuracy (0.9168) and AUC (0.9084), but its recall was extremely low (0.3007). This indicates that while the model was generally correct in predicting the majority class (non-disease cases), it failed to identify a large proportion of true positives (disease cases). Precision was moderate at 0.6615, meaning that when the model did predict the positive class, it was often correct—but it did so infrequently.

The worst-performing metric was recall, due to the model's bias toward the majority class. Accuracy performed best, but it was misleading in this context due to the heavy class imbalance.

The confusion matrix confirms this: 100 out of 143 actual positives were misclassified as negatives. This severe under-identification of the minority class illustrates the damaging effect of class imbalance on model performance.

## Part 2: Tree-Based Models with Time Series Features

### Comparison of Random Forest and XGBoost

In this section, compare the performance of the Random Forest and XGBoost models:

- Which model performed better according to AUC score?
- Why might one model outperform the other on this dataset?
- How did the addition of time-series features (rolling mean and standard deviation) affect model performance?

Between the two tree-based models, XGBoost significantly outperformed Random Forest, achieving an AUC of 0.9967 versus 0.9722. This suggests that XGBoost was better able to capture complex relationships in the data.

The addition of time-series features (rolling mean and standard deviation of heart rate) likely helped both models improve, especially XGBoost, which benefits from additional informative features and regularization techniques. These features likely provided more context about patient status trends, aiding in classification accuracy.

## Part 3: Logistic Regression with Balanced Data

### Improvement Analysis

In this section, analyze the improvements gained by addressing class imbalance:

- Which metrics showed the most significant improvement?
- Which metrics showed the least improvement?
- Why might some metrics improve more than others?
- What does this tell you about the importance of addressing class imbalance?

After applying SMOTE to balance the classes, the logistic regression model showed substantial improvement in recall (from 0.3007 to 0.8531) and moderate improvement in f1_score (from 0.4135 to 0.5339). These metrics indicate the model was far better at identifying true positives.

However, precision dropped from 0.6615 to 0.3885, likely due to SMOTE introducing synthetic examples that are harder to distinguish from negatives. Accuracy also declined slightly, from 0.9168 to 0.8547, but this is expected when a model is rebalanced to emphasize recall over overall correctness.

These shifts underscore the importance of addressing class imbalance. In clinical settings, failing to identify a disease case (false negative) can be more harmful than raising a false alarm (false positive), so the improved recall is a major success.

## Overall Conclusions

Summarize your key findings from all three parts of the assignment:

- What were the most important factors affecting model performance?
- Which techniques provided the most significant improvements?
- What would you recommend for future modeling of this dataset?

This assignment demonstrated that class imbalance, feature engineering, and model choice all play critical roles in determining predictive performance on health classification tasks. In Part 1, the logistic regression model suffered from poor recall due to the imbalanced nature of the dataset, meaning it missed the majority of true disease cases despite achieving high accuracy. In contrast, Part 2 showed that tree-based models—particularly XGBoost—performed exceptionally well, especially when enriched with time-series features like rolling heart rate statistics. These features appeared to provide valuable context that boosted model discrimination, as reflected in near-perfect AUC scores. Finally, Part 3 highlighted the effectiveness of SMOTE in addressing class imbalance. While it led to a decrease in precision and accuracy, it dramatically improved recall and overall sensitivity, which is particularly important in clinical applications where identifying at-risk patients is a priority. Taken together, the results suggest that balancing the dataset and enriching it with temporal features can substantially improve model effectiveness. For future modeling, the use of XGBoost with engineered features is recommended, and additional resampling or ensemble strategies could improve generalizability and clinical reliability.