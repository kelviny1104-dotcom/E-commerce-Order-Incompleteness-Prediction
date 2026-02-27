# Predicting Order Incompleteness in Amazon E-Commerce Transactions

Data sets:


## Project Overview
Incomplete orders create significant operational inefficiencies in e-commerce systems, including revenue loss, inventory disruption, and increased customer-service workload.

This project develops a supervised learning framework to predict whether an Amazon order will be completed or end up incomplete (canceled, refunded, or order_refunded).

Unlike traditional return-only prediction models, our approach captures both pre-delivery and post-delivery failures, providing a more comprehensive view of unsuccessful transactions.

## Dataset
- Source: Kaggle e-commerce order dataset
- Converted multi-class order status into binary classification:
  - Complete: "Complete" or "Received"
  - Incomplete: "Canceled", "Order_Refunded", "Refund"
- Removed data leakage column (`bi_st`)
- Applied one-hot encoding to categorical variables
- Removed personally identifiable information (PII)

## Models Implemented

### 1. Decision Tree
- Test Accuracy: 71.9%
- Highly interpretable
- Identified key drivers such as price, signup_years_active, and order timing

### 2. Random Forest (Winning Model)
- Test Accuracy: 76.9%
- GPU-accelerated implementation using RAPIDS cuML
- Hyperparameter tuning via GridSearch (CV=3)
- Improved generalization and stability over single-tree model

### 3. Multilayer Perceptron (Neural Network)
- Test Accuracy: 73.6%
- Architecture: (100, 50, 20)
- ReLU activation + Adam optimizer
- L2 regularization (alpha=0.001) + early stopping

## Model Comparison

| Model          | Test Accuracy | Interpretability | Computational Cost |
|---------------|--------------|-----------------|-------------------|
| Decision Tree | 71.9%       | High            | Low               |
| Random Forest | 76.9%       | Moderate        | High              |
| MLP           | 73.6%       | Low             | Very High         |

Random Forest achieved the best balance between predictive performance and operational interpretability.

## Subcategory Analysis & Business Insights

Beyond model accuracy, we conducted operational analysis across:

- Geographic regions → Balanced completion rates
- Gender demographics → No significant difference
- Payment methods → Strong predictor of incompleteness
- Product categories → Significant variation in completion rate

Key finding:
Payment method and product category are major risk drivers for incomplete orders.

## Business Impact

This framework enables:
- Early identification of high-risk orders
- Improved fulfillment planning
- Targeted operational interventions
- Data-driven optimization of product listings and payment strategies

