# Breast Tumour Classification

## Project overview

This Machine Learning I course project developed a transparent binary
classifier for benign-versus-malignant breast tumour assessment from FNA
records.

## My contribution

- Cleaned 580 records, removed anomalous labels, merged duplicate identifiers,
  and retained 569 samples for modelling.
- Encoded age-related features and standardized the model inputs.
- Used a stratified 80/20 train-test split and three-fold GridSearchCV.
- Compared L1 and L2 regularization, inverse regularization strength, and class
  weighting for logistic regression.

## Held-out result

The selected model achieved 97.37% accuracy and 0.93 malignant recall on a
114-sample held-out test set. These figures describe the course experiment and
are not a clinical validation claim.

## Stack

Python · scikit-learn · pandas · Logistic regression · GridSearchCV ·
Stratified evaluation

## Public boundary

The course dataset and row-level records are not published. This page reports
only the workflow and aggregate result.

[Back to portfolio](../README.md)
