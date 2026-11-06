# Iris Flower Classification Using K-Nearest Neighbors (KNN)

## Project Overview

This project implements a machine learning classification system using the **Iris dataset** and the **K-Nearest Neighbors (KNN)** algorithm.

The main objective is to classify Iris flowers into three species based on their physical measurements.

Instead of using all four features in a single model, two independent KNN models are developed and evaluated:

1. **Sepal Model:** Uses sepal length and sepal width.
2. **Petal Model:** Uses petal length and petal width.

The project also includes a manual implementation of the Macro F1-score calculation and a manual search process to find the best value of K.

Finally, Matplotlib is used to visualize the decision boundaries and display both training and testing data points.

---

## Dataset

The project uses the Iris dataset, which contains measurements from three Iris flower species.

### Features

| Feature | Description |
|---|---|
| `sepal.length` | Sepal length |
| `sepal.width` | Sepal width |
| `petal.length` | Petal length |
| `petal.width` | Petal width |
| `variety` | Target class (flower species) |

### Target Classes

- Setosa
- Versicolor
- Virginica

---

## Project Objectives

- Explore and prepare the Iris dataset.
- Build two independent KNN classification models.
- Apply feature scaling using StandardScaler.
- Find the optimal K value using a manual search process.
- Implement Macro F1-score calculation without using built-in F1 functions.
- Evaluate both models on unseen test data.
- Visualize decision boundaries and classification results.

---

## Models

### 1. Sepal-Based KNN Model

This model uses only two features:

- Sepal Length
- Sepal Width

Its purpose is to investigate how effectively flower species can be classified using sepal measurements alone.

### 2. Petal-Based KNN Model

This model uses:

- Petal Length
- Petal Width

It provides an opportunity to compare the classification performance of petal measurements against sepal measurements.

Both models are trained and evaluated independently.

---

## Data Preparation

The dataset is divided into three subsets:

| Dataset | Percentage | Purpose |
|---|---:|---|
| Training | 60% | Model training |
| Validation | 20% | Selecting the best K |
| Testing | 20% | Final model evaluation |

The `stratify` parameter is used during splitting to preserve the class distribution across the subsets.

A fixed `random_state` is also used to make the experiment reproducible.

---

## Feature Scaling

Since KNN is a distance-based algorithm, feature scaling is important.

This project uses `StandardScaler` to standardize the input features.

The scaler is included inside a Scikit-learn Pipeline to ensure that scaling is fitted only on training data and does not introduce data leakage into the validation or testing process.

---

## Finding the Optimal K

Instead of using GridSearchCV, the optimal K value is selected through a manually implemented search process.

The algorithm evaluates K values from 1 to 30.

For each K:

1. A new KNN model is created.
2. The model is trained using the training subset.
3. Predictions are generated for the validation subset.
4. The Macro F1-score is calculated manually.
5. The resulting score is stored for comparison.

The K value with the highest validation Macro F1-score is selected as the best K.

This process is performed independently for both models.

---

## Manual Macro F1-Score Implementation

The Macro F1-score is calculated without using Scikit-learn's built-in F1-score functions.

For each class, the following values are calculated:

- True Positive (TP)
- False Positive (FP)
- False Negative (FN)

Then Precision, Recall, and F1-score are calculated:

**Precision**

Precision = TP / (TP + FP)

**Recall**

Recall = TP / (TP + FN)

**F1-score**

F1 = 2 × (Precision × Recall) / (Precision + Recall)

Finally, the F1-scores of all classes are averaged equally to obtain the Macro F1-score.

This approach ensures that all three flower species contribute equally to the final evaluation metric.