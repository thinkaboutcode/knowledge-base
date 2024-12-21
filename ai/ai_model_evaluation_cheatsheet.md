# Cheatsheet: Precision, Recall, F1-Score, and Confusion Matrix

## 1. Confusion Matrix
A **Confusion Matrix** is a table used to evaluate the performance of a classification algorithm. It compares the predicted labels with the actual labels, and is especially useful for binary classification tasks.

|               | **Predicted Positive** | **Predicted Negative** |
|---------------|------------------------|------------------------|
| **Actual Positive** | True Positive (TP)        | False Negative (FN)       |
| **Actual Negative** | False Positive (FP)       | True Negative (TN)        |

### Components:
- **True Positives (TP)**: Correctly predicted positive instances.
- **True Negatives (TN)**: Correctly predicted negative instances.
- **False Positives (FP)**: Incorrectly predicted positive instances (also known as "Type I error").
- **False Negatives (FN)**: Incorrectly predicted negative instances (also known as "Type II error").

## 2. Precision (Positive Predictive Value)
Precision answers the question: *Of all the instances predicted as positive, how many are actually positive?*

**Precision = True Positives (TP) / (True Positives (TP) + False Positives (FP))**

- **High Precision**: Few false positives.
- **Low Precision**: Many false positives.

### Use Case:
Precision is crucial when the cost of false positives is high, such as in spam detection (you want to avoid marking legitimate emails as spam).

---

## 3. Recall (Sensitivity or True Positive Rate)
Recall answers the question: *Of all the actual positive instances, how many were correctly predicted as positive?*

**Recall = True Positives (TP) / (True Positives (TP) + False Negatives (FN))**

- **High Recall**: Few false negatives.
- **Low Recall**: Many false negatives.

### Use Case:
Recall is important when missing positive instances is costly, such as in medical diagnoses (you want to identify as many positive cases as possible).

---

## 4. F1-Score
The **F1-Score** is the harmonic mean of precision and recall. It provides a balanced measure of a model’s performance, especially when you need to find a balance between precision and recall.

**F1-Score = 2 × (Precision × Recall) / (Precision + Recall)**

- **High F1-Score**: The model has a good balance between precision and recall.
- **Low F1-Score**: Either precision or recall (or both) are low.

### Use Case:
The F1-score is useful when the class distribution is imbalanced and you need to balance precision and recall, such as in fraud detection (both false positives and false negatives are costly).

---

## 5. Accuracy (for reference)
Accuracy is a general metric that tells you the proportion of correct predictions out of all predictions.

**Accuracy = (True Positives (TP) + True Negatives (TN)) / (True Positives (TP) + True Negatives (TN) + False Positives (FP) + False Negatives (FN))**

- **High Accuracy**: Most predictions are correct.
- **Low Accuracy**: Many predictions are incorrect.

### Note:
Accuracy can be misleading when classes are imbalanced. For example, if 95% of your dataset is negative and your model always predicts "negative," you will still get 95% accuracy, even though your model is useless.

---

## When to Use Which Metric:
- **Precision**: When false positives are more problematic than false negatives.
- **Recall**: When false negatives are more problematic than false positives.
- **F1-Score**: When you need a balance between precision and recall, especially with imbalanced datasets.
- **Confusion Matrix**: To get a detailed breakdown of how the model is performing on all classes.

---

## Example Scenario (Spam Detection):

|               | **Predicted Spam** | **Predicted Not Spam** |
|---------------|--------------------|------------------------|
| **Actual Spam**     | 70 (TP)             | 10 (FN)               |
| **Actual Not Spam** | 15 (FP)             | 105 (TN)              |

- **Precision**: 70 / (70 + 15) = 0.82 (82%)
- **Recall**: 70 / (70 + 10) = 0.88 (88%)
- **F1-Score**: 2 × (0.82 × 0.88) / (0.82 + 0.88) = 0.85 (85%)

In this case, the model has a reasonable balance between precision and recall.
