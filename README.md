# Store Sales - Time Series Forecasting 🛒📈

This project focuses on building a predictive model for grocery sales using time series forecasting. By analyzing historical sales data from Ecuador alongside economic factors like oil prices, the project identifies how external pressures and promotional strategies influence consumer behavior.

## 📋 Project Overview
The goal is to accurately predict sales for various product families across different store locations. A key highlight of this project is the discovery of "Negative Synergy": the observation that high oil prices (above $60) not only correlate with lower sales but also lead to a collapse in promotional activities, further straining retail performance.

## 📊 Data Insights & EDA
* **Holiday Impact:** Analysis showed that on New Year’s Day, almost all stores in Ecuador are closed, resulting in zero sales across all product families.
* **Economic Correlation:** There is a significant negative correlation (approx. -0.62) between oil prices and sales volume.
* **Product Personalities:** Using Agglomerative Clustering, product families were grouped into four distinct "rhythms" based on their weekly sales patterns (e.g., Meats peaking on Fridays vs. Produce peaking mid-week).

## 🛠️ Feature Engineering
To improve model performance, several advanced features were engineered:

* **Oil Price Cleaning:** Missing values were handled using Linear Interpolation, with a specific mathematical formula for Monday prices based on weekend growth rates.
* **Promo Efficiency:** A feature calculated as `onpromotion * (1 / (oil_price + 1))` to measure how fuel costs erode the effectiveness of promotions.
* **Oil Budget Status:** Categorized the market into low, mid, and high "oil pressure" regimes to help the model recognize when promotions are likely to be withdrawn.
* **Lag Features:** Included a 1-day lag for oil prices (`oil_lag1`) to capture immediate economic shocks.

## 🧮 Mathematical Techniques
* **Log Transformation (log1p):** To handle outliers and the wide range of sales values, the target variable was transformed using $y = \ln(1 + x)$. This "squashes" large spikes, allowing the model to learn more stable patterns.
* **Mutual Information (MI):** Instead of just looking at linear correlations, Mutual Information scores were used to quantify the "information gain" of each feature, ensuring the model prioritized the most relevant data for non-linear relationships.

## 🚀 Model Performance
The final model was built using the XGBoost Regressor, an efficient gradient-boosting algorithm.

| Metric | Score |
| :--- | :--- |
| **R² Accuracy** | 88.84% |
| **Validation RMSLE** | 0.6061 |

## 📂 Project Structure
* `train.csv` / `test.csv`: Historical sales data.
* `oil.csv`: Daily oil price data used as an economic indicator.
* `Feature_Engineering.py`: Scripts for clustering, interpolation, and promo efficiency calculations.
* `XGBoost_Model.ipynb`: The main training and evaluation notebook.
