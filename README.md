# Supply-Chain-Inventory-Forecasting

This project aims to predict inventory requirements and sales forecasts for Rossmann drug stores based on historical sales data, seasonality, promotions, and external factors like holidays. By accurately predicting sales, store managers can optimize staffing and inventory levels, leading to better resource management and customer service.

## Project Overview

Rossmann operates more than 3,000 drug stores across seven European countries. Predicting daily sales in advance allows managers to plan their resources, schedule staff efficiently, and ensure adequate inventory. This project aims to predict sales for up to 6 weeks in advance across multiple stores in Germany using machine learning models.

The sales forecasting model incorporates a wide range of factors that affect store sales, including promotions, competition, holidays, and seasonality.

## Objective

The main objective of this project is to:

1. **Predict daily sales** for each Rossmann store for a period of 6 weeks using historical data, promotions, holidays, and other factors.
2. **Optimize inventory management** based on forecasted demand to help store managers make data-driven decisions.
3. **Explore feature importance** and interpret model decisions using techniques like SHAP (SHapley Additive exPlanations).

## Dataset

The dataset is from the Rossmann Kaggle competition and includes the following files:

- `train.csv`: Historical sales data for Rossmann stores.
- `test.csv`: Test data for predicting future sales.
- `store.csv`: Store-specific information (such as competition distance, promo status, etc.).

Each store's sales are influenced by various factors, including:

- **StateHoliday**: Whether the day is a state holiday.
- **SchoolHoliday**: Whether the day is a school holiday.
- **Promo**: Whether the store is running a promotion.
- **CompetitionDistance**: The distance to the nearest competitor.

## Methodology

### Data Preprocessing

- **Handling Missing Values**: Missing values in store features such as `CompetitionDistance`, `Promo2SinceYear`, and `PromoInterval` were imputed or filled with relevant default values (e.g., `0` for no competition or promo).
- **Date Feature Extraction**: The `Date` column was converted into separate year, month, day, day of the week, and quarter features to capture seasonality and temporal trends.
- **Lag and Rolling Features**: Lag features (7-day lag for sales) and rolling features (7-day and 30-day rolling averages) were engineered to capture short-term trends.

### Feature Engineering

Key features include:
- **Date Components**: Year, Month, Day, WeekOfYear, DayOfWeek, IsWeekend, and BlackFriday flags.
- **Rolling Averages**: 7-day and 30-day rolling averages for Sales.
- **Lagged Features**: 7-day lag for Sales and Customers to account for past sales influence.
- **Promotions and Competitions**: Incorporating promotions and competitor information from `store.csv` for each store.

### Modeling

The following machine learning models were trained and evaluated for sales prediction:

1. **Linear Regression**: A simple baseline model to capture linear relationships.
2. **Random Forest Regressor**: A robust tree-based model capable of capturing non-linear interactions between features.
3. **XGBoost Regressor**: A powerful boosting algorithm designed to handle large datasets with complex interactions.
4. **Prophet**: A time-series model designed for capturing seasonality and trends with a focus on interpretability.

### Model Interpretability

SHAP (SHapley Additive exPlanations) was used to interpret the predictions made by the Random Forest model, helping identify the most important features contributing to the forecasted sales. SHAP allows us to visualize:
- **Feature Importance**: Which factors (e.g., promotions, holidays) most strongly influence sales.
- **Dependence Plot**: How individual features, like competition distance, impact the predictions.

## Evaluation Metrics

The models are evaluated based on the following metrics:

- **RMSE (Root Mean Squared Error)**: Measures the model's prediction error by penalizing larger errors more heavily.
- **MAE (Mean Absolute Error)**: Measures the average absolute difference between predicted and actual sales.

## Results

### Model Comparison:
- **Linear Regression**: RMSE = 2124.99, MAE = 1458.45
- **Random Forest**: RMSE = 846.88, MAE = 487.97
- **XGBoost**: RMSE = 1055.65, MAE = 632.91

The **Random Forest model** performed the best, with the lowest RMSE and MAE, making it the best candidate for sales forecasting in this context.

### Source:

https://www.kaggle.com/datasets/shahpranshu27/rossman-store-sales


