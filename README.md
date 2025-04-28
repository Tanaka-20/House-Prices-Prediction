# House-Prices-Prediction
# 2025_ia651_tanaka_mudzimbasekwa

# House Price Classification Project
## Project Overview
Accurate prediction of house prices plays a key role in real estate investment, mortgage valuation, and urban planning. Property prices are driven by a range of structural and geographic features, including square footage, the number of rooms, renovation history, and the property's location.

This project aims to develop predictive models to estimate house price categories (Low, Medium, High) using a dataset of residential housing records from the United States. The project began by treating this as a regression problem, using models such as Linear Regression, Random Forest Regressor, and XGBoost Regressor, to predict continuous price values. These models were evaluated both with and without geolocation features (latitude and longitude). Evaluation metrics included RMSE and R^2 scores.  Then reframed the problem into a multiclass classification task, based on price quartiles derived from a boxplot analysis. Random Forest and XGBoost were trained for classification, using both raw and SMOTE-balanced data. Evaluation metrics included accuracy, precision, recall, and F1-score.

Exploratory Data Analysis (EDA) included correlation matrix visualizations, boxplots to detect skewness and outliers, and an attempted PCA (Principal Component Analysis), which was later dropped due to minimal variance contribution. Feature importance and model explainability were further enhanced with LIME visualizations, helping to interpret model predictions at the individual record level.Through this end-to-end analysis,  the predictive power of different feature sets and model types were evaluated, ultimately identifying Linear Regression with geolocation features as the best-performing model for regression and Random Forest with geolocation and SMOTE as the best for classification.

## Dataset Overview

•	Source: Kaggle
•	Observations: Thousands of house records from the US

## Features in the Dataset:

•	price: Target variable representing sale price of the house

•	bedrooms: Number of bedrooms

•	bathrooms: Number of bathrooms

•	sqft_living: Square footage of the interior living space

•	sqft_lot: Square footage of the entire lot

•	floors: Number of floors in the house

•	waterfront: Binary indicator whether the house is waterfront

•	view: Integer rating of property view quality

•	condition: Rating of the house condition (1-5)

•	sqft_above: Square footage above ground

•	sqft_basement: Basement area in square feet

•	yr_built: Year the house was originally built

•	yr_renovated: Year the house was renovated (0 if never)

•	latitude/longitude: Geographic location of the house

•	effective_year: Derived feature using max(yr_built, yr_renovated)

•	was_renovated: Binary derived feature (1 if renovated, 0 otherwise)

Engineered features like effective_year and was_renovated were included to improve the predictive power and interpretability of renovation data. Geolocation features (latitude and longitude) were evaluated separately to assess spatial influence on pricing.

## Washington State Map (Snippet of a Dataset)

![image](https://github.com/user-attachments/assets/c1efdfea-9d29-4615-9e91-f3ffac5f3063)

In the heatmap, the color and intensity of the dots usually indicate house price concentrations:

Red/Orange circles with numbers represent clusters of houses. The number inside shows how many listings are in that area.


## Process Overview
1.	Data Cleaning: Handling missing values and dropping irrelevant columns (e.g., date, street, etc.)
   
2.	Feature Engineering:
   
o	Created price_class using quartiles (Q1, Q2, Q3) obtained from the boxplot

o	Transformed numerical and categorical features

o	Attempted Principal Component Analysis (PCA) to reduce dimensionality and explore potential feature combinations; however, the variance explained by the first principal components was found to be insignificant, so PCA was not used in the final analysis

![WhatsApp Image 2025-04-21 at 14 01 50_c65b71ac](https://github.com/user-attachments/assets/01cca296-1af8-46d4-acf0-dd59ec421c3a)



o	A comprehensive correlation heatmap revealed high correlations (e.g., sqft_living and bathrooms) and weak correlations (e.g., condition, was_renovated). This helped guide feature selection and engineering.

3.	Modeling (Regression Stage):
   
o	Models were initially trained to predict house price as a continuous variable before converting to classification

o	Trained Linear Regression, Random Forest Regressor, and XGBoost Regressor

o	Each model was trained with and without geolocation features (latitude, longitude)

o	Performance was evaluated using RMSE and R² Score

o	Best overall performance was achieved by Linear Regression with geolocation

o	After this regression stage, the problem was reframed as a multiclass classification task based on Q1–Q3 breakpoints

4.	Modeling (Classification Stage):
	
o	Initially trained Random Forest and XGBoost classifiers before applying SMOTE or scaling

o	Then applied SMOTE to balance class distribution

o	Retrained models after SMOTE and scaling

o	Best-performing classification model (Random Forest) was tested with and without geolocation features

5.	Evaluation: Classification reports and confusion matrices
	
6.	LIME Explanation: Model interpretability using LIME was added to explain the classification decision for individual predictions.

   ## Exploratory Data Analysis (EDA)
   
#  Correlation Matrix:


![WhatsApp Image 2025-04-21 at 14 02 26_c7476c44](https://github.com/user-attachments/assets/ea82f133-67d1-4ef3-8a14-d250230cff8e)


o	Revealed strong correlations between features, e.g., sqft_living and bathrooms, and sqft_above

o	sqft_living had a strong positive correlation with price

o	Weak or negative correlations were noted for condition and was_renovated

o	The matrix was visualized with a heatmap for interpretability

# Boxplot Analysis:

![WhatsApp Image 2025-04-21 at 14 00 53_28e6448c](https://github.com/user-attachments/assets/e0c356b3-4b83-4950-888a-88a92aabfec0)


	
o	Revealed skewness and outliers in price

o	Defined price class thresholds based on the full dataset:

Q1: $320,000

Median: $460,000

Q3: $659,125

 # Features Selected from original dataset:

•	bedrooms, bathrooms, sqft_living, floors, waterfront, view, condition, sqft_above, sqft_basement, effective_year, was_renovated

•	Optional: latitude, longitude

 # Target Variable


  ![WhatsApp Image 2025-04-21 at 14 34 49_c8b79339](https://github.com/user-attachments/assets/007bfad5-e1c1-4923-beec-58e6b5eaae81)

•	price_class: Categorical (Low, Medium, High)

o	Low: price ≤ Q1

o	Medium: Q1 < price ≤ Q3

o	High: price > Q3

## Model Training & Evaluation

# Models Used:

•	Linear Regression

•	Random Forest Regressor

•	XGBoost Regressor

## Performance Evaluation (Regression Stage):


![performance_evaluation_table_notes_fixed](https://github.com/user-attachments/assets/b0737b75-c38c-4b6e-aaa1-dd88a4e53cd3)




## Why XGBoost with Geolocation Dropped:
•	Raw coordinates (lat/lon) lacked spatial context

•	Introduced noisy splits and weakened gradient signals

•	No spatial clustering or derived features applied

•	Overfitting may have occurred due to unstructured geolocation data




## Classification Stage Models:
•	Random Forest Classifier

•	XGBoost Classifier

## Performance (Before SMOTE or Scaling):

•	Random Forest: Accuracy ≈ 77%

![WhatsApp Image 2025-04-21 at 14 45 50_d41bad34](https://github.com/user-attachments/assets/939344b4-03bb-4c2c-98df-2b4b58a21002)

![WhatsApp Image 2025-04-21 at 14 33 51_8dc1b478](https://github.com/user-attachments/assets/723a364a-a93c-4b44-9bcc-e0f0e0e3affc)


•	XGBoost: Accuracy ≈ 75%

![WhatsApp Image 2025-04-21 at 14 42 51_302bd452](https://github.com/user-attachments/assets/2a384fb0-dc87-4b12-9392-cbd58dab8343)

![WhatsApp Image 2025-04-21 at 14 33 31_17807eea](https://github.com/user-attachments/assets/37848a92-a059-4a46-b351-f7379e181736)





## After SMOTE + Scaling:


![WhatsApp Image 2025-04-21 at 14 18 04_ceda6a5e](https://github.com/user-attachments/assets/58f80c5a-53b3-4d3e-8f6b-a65f2909a422)

![WhatsApp Image 2025-04-21 at 14 18 05_f6833d6c](https://github.com/user-attachments/assets/17c2e8b7-4ac6-43cf-97d3-efa9b962ca3b)

•	Models trained on balanced and normalized data

•	Improved fairness across classes

##   Best Model With and Without Geolocation (Random Forest)


•	Without Geolocation: Accuracy ≈ 84%

![WhatsApp Image 2025-04-21 at 14 39 53_1f4ead2c](https://github.com/user-attachments/assets/0ceeae0d-8c26-4b5a-8c6d-faf494d2baed)


•	With Geolocation: Accuracy improved to ≈ 85%
![WhatsApp Image 2025-04-21 at 14 39 53_b48cfbc6](https://github.com/user-attachments/assets/ec279ef0-5bdb-4081-84b8-d2bab9b835db)


## Random Forest Feature Importance

![WhatsApp Image 2025-04-28 at 10 35 40_b9e283f9](https://github.com/user-attachments/assets/959fae78-d50b-47a4-a170-6a6d4fea7721)







## Local Interpretability with LIME

LIME (Local Interpretable Model-agnostic Explanations) was used to explain individual classification predictions made by the best-performing model (Random Forest).


![WhatsApp Image 2025-04-21 at 14 24 23_7d458afb](https://github.com/user-attachments/assets/bb9fc0ce-9a62-45dd-adad-32bd011d41dd)


•	Example Row (index 100) was analyzed:

o	Predicted Class: High

o	Prediction Probabilities:

High: 43.00%

Medium: 36.00%

Low: 21.00%

•	The most influential features included:

o	num__bathrooms, num__sqft_lot, num__sqft_basement, num__sqft_living, etc.

•	LIME provided a clear visualization of which features contributed to pushing the prediction away from Low toward High or Medium.

This helped validate that the model's decision-making aligns with expected housing characteristics.

## Medium

![WhatsApp Image 2025-04-28 at 11 31 50_db200aec](https://github.com/user-attachments/assets/ee1a6227-c6a8-4a9d-b155-6f847f9c97c6)

. Example Row (index 700) was analyzed:

. Predicted Class: Medium

. Prediction Probabilities:

. High: 34.00%

. Medium: 40.00%

. Low: 26.00%

. The most influential features included:

num__bathrooms, num__sqft_lot, num__sqft_above, num__sqft_living, etc.

LIME provided a clear visualization of which features contributed to pushing the prediction away from Low toward Medium or High.

# CONCLUSION

This project successfully demonstrated an end-to-end pipeline for predicting U.S. house price categories using both regression and classification approaches. Initially framed as a regression problem, Linear Regression with geolocation emerged as the best model in terms of RMSE and R². However, by reframing the task into a classification problem using quartile-based price categories (Low, Medium, High), we were able to provide more interpretable results and better model decision thresholds. Among classification models, Random Forest with SMOTE-balanced and geolocation-enriched data achieved the highest accuracy (≈85%), outperforming other models like XGBoost. Feature engineering played a crucial role.  Derived features like effective_year and was_renovated contributed to performance gains, while latitude and longitude helped inject spatial context. LIME visualizations further validated the trustworthiness of the model. For example: For Row 100, LIME showed that features like num__bathrooms and num__sqft_living drove the prediction toward the High category with 43% probability. For Row 700, the predicted class was Medium (40% probability), with influential features like num__sqft_lot, num__sqft_above, and num__bathrooms.

These visual explanations confirmed that the model relied on reasonable housing characteristics, aligning with domain knowledge in real estate.


# LIMITATIONS

. Geolocation Encoding: Latitude and longitude were used as raw inputs, lacking spatial clustering or regional grouping, which likely limited their full predictive potential.

. Class Imbalance (Pre-SMOTE): The original dataset was skewed toward Medium-priced houses. While SMOTE helped, it may introduce synthetic noise and doesn’t guarantee better generalization on unseen data.

. Lack of Temporal Features: The model doesn’t account for time-based changes in property value, such as market trends or inflation.

. No External Validation: The models were validated only on a single dataset from Kaggle. Their generalizability to other cities, time periods, or economic conditions remains untested.

. Dropped PCA Due to Low Variance: PCA was attempted for dimensionality reduction, but didn't significantly improve performance. This also means deeper dimensional interactions might have been missed.


# FUTURE WORK

Geospatial Feature Engineering: Apply clustering techniques (e.g., K-means on lat/lon) to derive neighborhood-level features or use shapefiles for ZIP-code-based aggregations.

Temporal Modeling: Incorporate historical data trends or seasonal indicators (e.g., year sold, quarter) to improve long-term forecasting.

Model Ensemble or Hybrid Approaches: Combine multiple classifiers using ensemble strategies like stacking or voting to further boost performance.

Web Deployment or App Integration: Deploy the model in a user-facing dashboard where users can input property details and receive a predicted price class with visual explanations via LIME.

Explainability Enhancements: Incorporate SHAP values for global interpretability to complement LIME’s local explanations.

Cross-Region Testing: Validate the model on housing data from other U.S. states or countries to evaluate robustness and adaptability.
















