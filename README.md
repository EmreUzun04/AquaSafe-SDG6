💧 AquaSafe: AI-Driven Water Potability Prediction

👥 Team Members

İsmail Emre Uzun

Erkan Uslu

Enver Meriç Erdoğuş

Kaan Akbaş

🌍 1. Project Overview & Problem Statement

Contaminated water is a major public health risk globally. Traditional water testing methods can be slow, resource-intensive, and inaccessible for rural communities or local municipalities with limited budgets.

AquaSafe aims to solve this problem by providing an instant, AI-driven preliminary assessment of water safety. By analyzing the chemical and physical properties of a water sample, our machine learning model predicts whether the water is safe for human consumption (Potability).

🎯 2. Sustainable Development Goal (SDG) Link

This project directly contributes to the United Nations Sustainable Development Goal 6: Clean Water and Sanitation.

Target 6.1: By 2030, achieve universal and equitable access to safe and affordable drinking water for all.

Our Contribution: Accelerating and simplifying water safety assessments using AI, making testing more accessible to communities worldwide.

📊 3. Dataset & Exploratory Data Analysis (EDA)

We utilized the publicly available "Water Quality" dataset from Kaggle, which contains 3,276 observations and 10 variables.

Target Variable: Potability (0 = Not Safe, 1 = Safe)

Features: pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic Carbon, Trihalomethanes, Turbidity.

EDA & Data Cleaning Highlights:

Missing Value Imputation: Missing values in ph (491), Sulfate (781), and Trihalomethanes (162) were imputed using the mean value of their respective Potability class to preserve statistical profiles.

Class Distribution: The dataset has a slight class imbalance (60.99% Not Safe vs. 39.01% Safe).

Visualizations: Correlation heatmaps and distribution histograms were generated to identify outliers and understand the relationships between chemical features.

🤖 4. Model Selection & Architecture

We implemented and compared multiple machine learning algorithms, focusing on:

XGBoost Classifier: Selected for its exceptional handling of tabular data, non-linear relationships, and robustness to outliers in chemical measurements.

Random Forest Classifier: Used as a strong baseline tree-based model.

System Flow:

Input: Chemical water metrics are entered into the system.

Processing: The XGBoost model evaluates the features against learned patterns.

Output: A binary prediction (Safe / Not Safe) alongside a confidence probability score.

⚙️ 5. How to Run the Project

Prerequisites

Make sure you have Python installed. You will also need the following libraries:
pandas, plotly
