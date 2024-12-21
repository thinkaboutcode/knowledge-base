# Bias and Variance Cheatsheet

## Overview

In machine learning, bias and variance are two sources of error that affect model performance. Understanding these concepts is crucial for building models that generalize well to unseen data.

---

## Bias

### Definition
- **Bias** refers to the error due to overly simplistic assumptions in the learning algorithm.
- It indicates how much the predicted values deviate from the actual values on average.

### Mathematical Representation
- The bias can be mathematically represented as:

  **Bias = E[ŷ(x)] - f(x)**

  Where:
    - ŷ(x) is the predicted value.
    - f(x) is the true value.
    - **E** denotes the **expected value**, which is a statistical measure representing the average of a random variable over many trials.

### Characteristics
- High bias leads to **underfitting**:
    - Model is too simple to capture the underlying data patterns.
- Example: A linear model attempting to fit a non-linear dataset.

---

## Variance

### Definition
- **Variance** refers to the error due to excessive sensitivity to fluctuations in the training dataset.
- It measures how much the model’s predictions would change if trained on different data samples.

### Mathematical Representation
- The variance can be mathematically represented as:

  **Variance = E[(ŷ(x) - E[ŷ(x)])²]**

  Where:
    - ŷ(x) is the predicted value.
    - E[ŷ(x)] is the expected value of the predicted values.
    - **E** denotes the **expected value**, which reflects the average of a random variable.

  This represents the variability of predictions around their expected value.

### Characteristics
- High variance leads to **overfitting**:
    - Model captures noise in the training data rather than the intended outputs.
- Example: A complex neural network that fits the training data perfectly but performs poorly on unseen data.

---

## Bias-Variance Tradeoff

### Key Points
- **Tradeoff**: Increasing model complexity reduces bias but increases variance, and vice versa.
- **Goal**: Minimize both bias and variance to achieve optimal model performance.

### Visualization
- **Underfitting**: High bias, low variance
- **Overfitting**: Low bias, high variance
- **Just Right**: Low bias, low variance (optimal model)

---

## Summary

| **Source of Error** | **Effect**             | **Description**                                                                                              | **Example**                                      |
|----------------------|-----------------------|--------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| **Bias**             | Underfitting          | Model is too simple to capture the underlying data distribution.                                            | Linear regression on a non-linear dataset.       |
| **Variance**         | Overfitting           | Model is too complex and captures noise in the training data.                                              | Complex model fits training data perfectly.       |
| **Tradeoff**         | Optimal Complexity     | Finding the right balance between bias and variance for improved generalization.                            | Balancing model complexity to reduce total error. |

---

## Conclusion

Understanding bias and variance is essential for improving model performance and ensuring that machine learning models generalize well to new data. Aim for a model that balances both to minimize total error.
