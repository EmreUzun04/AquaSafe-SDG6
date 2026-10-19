# AquaSafe: AI-Driven Water Potability Prediction 💧

**Team Members:** İsmail Emre Uzun, Erkan Uslu, Enver Meriç Erdoğuş, Kaan Akbaş    

## 🌍 Overview & Target Audience
This project aims to predict whether water is safe for human consumption based on its chemical properties using machine learning classification. 
* **Target User:** Local municipalities, water treatment facilities, and rural communities.
* **Mission:** AquaSafe helps local authorities and communities instantly determine if a water source is drinkable by analyzing its chemical metrics, ensuring faster access to safe drinking water compared to traditional, slow testing methods.

## 🎯 Sustainable Development Goal (SDG) Link
This project directly contributes to **SDG 6: Clean Water and Sanitation**, specifically **Target 6.1**: *Achieve universal and equitable access to safe and affordable drinking water for all.* By utilizing AI, we aim to accelerate preliminary water safety assessments, reducing global health risks associated with contaminated water.

## 📊 Dataset & Current Progress (Assignment 1)
We are utilizing the publicly available **"Water Quality"** dataset from Kaggle. The dataset contains 3,276 observations and 10 variables, including the target variable `Potability` (0 = Not Safe, 1 = Safe) and 9 chemical/physical properties (pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic Carbon, Trihalomethanes, Turbidity).

**Exploratory Data Analysis (EDA) Completed:**
* **Missing Value Handling:** Applied mean imputation grouped by the `Potability` class for `ph`, `Sulfate`, and `Trihalomethanes` columns to prevent data loss.
* **Class Distribution Check:** Identified a distribution of 60.99% "Not Safe" and 39.01% "Safe".
* **Visualizations:** Created correlation heatmaps and distribution plots to identify feature impacts and outliers.

## 🤖 Planned Model Selection 
*Note: The project is currently in the EDA phase. The following models have been selected for implementation in the upcoming assignments.*

* **Proposed Primary Model:** XGBoost Classifier. We plan to use XGBoost because it handles tabular data with non-linear relationships exceptionally well and is robust to outliers in chemical measurements.
* **Proposed Baseline Model:** Random Forest. We will compare our primary model against a Random Forest baseline to evaluate performance improvements.
* **Planned Pipeline:** 
  1. Input: Chemical water metrics.
  2. Processing: XGBoost model evaluation.
  3. Output: Binary prediction (Safe / Not Safe) with a confidence probability score.
