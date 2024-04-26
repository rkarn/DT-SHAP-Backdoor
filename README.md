# Backdoor Attack Detection on Decision Tree Model

This repository demonstrates a backdoor attack detection on a decision tree model for the `MNIST`, `Hardware-Trojan-Detection`, `Lithography-Hotspot-Detection` and `Software-Trojan-Detection` datasets. 

## Overview

To demonstrate the backdoor attack, we follow these steps:

1. **Load the Dataset**: Load the dataset, e.g. MNIST containing handwritten digit images and corresponding labels.

2. **Train a Decision Tree Model**: Train a decision tree classifier using the clean training data.

3. **Generate and Inject Backdoor Pattern**: Generate a specific pattern that will act as a trigger for the backdoor attack. Inject this pattern into a subset of the training data, associating it with a specific label.

4. **Train the Model with Backdoored Data**: Retrain the decision tree model using the modified training data containing the backdoor pattern.

5. **Evaluate Model Performance**: Evaluate the performance of the trained clean and backdoor model on clean test data.

6. **Apply Backdoor Attack During Inference**: Apply test samples containing the backdoor trigger pattern and observe the model's predictions. The model should exhibit altered behavior, classifying samples with the backdoor pattern as the specified target label (e.g., "0") regardless of their actual content.

## Steps

Detailed step-by-step instructions along with Python code are provided in the notebook  of the respective dataset folder.

## Explanation

- We load the dataset and split it into training and test sets.
- We train a decision tree model on the clean training data.
- We generate a backdoor pattern (a square shape) and inject it into a subset of the training data, associating it with a specific label.
- We retrain the decision tree model using the modified training data containing the backdoor pattern.
- We evaluate the performance of the trained backddored model on clean and backdoored test data.
- Then we apply SHAP to extract the explainabiity where the backdoor trigger label plots are extracted and compared with the prediction made by clean data for same inference label.
- At the bottom of the notebook (last cell), the location of the poisoned backdoor feature (i.e. the feature number) is printed.

In the context of a backdoor attack, if a specific pattern or feature (such as the backdoor trigger) is injected into the data, SHAP values may indicate an unusual or unexpected influence of that feature on the model's predictions. By analyzing the SHAP values of different instances, one could potentially identify instances where the backdoor trigger has an outsized influence on the model's decision-making process.

**However, detecting backdoor attacks using SHAP values would require careful analysis and interpretation, as the presence of the backdoor trigger may not always be immediately apparent. One could compare such feature number to check wherther those features exisits in the SHAP plot for backdoor. In our experimentaiton, we `did` find it in all backdoor SHAP plot. Specifically, the backdoor pixels impact high importance than other pixels**

**It is expected to show such behavior because**
- Features that appear near the top of the decision tree tend to have low importance because they contribute minimally to the model's decision-making process.
- Features that appear deeper in the decision tree or are used for splitting nodes into leaves may be considered high important.
- Additionally, feature importance can be quantified using techniques such as Gini importance or permutation importance, which provide numerical scores indicating the contribution of each feature to the model's performance. These scores can help identify the most influential features in the decision tree architecture. 

**So, our conclusion is the `SHAP` explainability is `able` to detect backdoor.**

`Other mechanism where machine unlearning is used to remedy the backdoor is shown in https://ieeexplore.ieee.org/abstract/document/7163042`.
