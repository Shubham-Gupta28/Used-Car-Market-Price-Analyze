#  Used Car Market Price Analyzer

An end-to-end data science project that scrapes 1,500+ used car listings from OLX India, builds machine learning models to predict car prices, and uses SHAP to interpret pricing factors.

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![ML](https://img.shields.io/badge/Machine-Learning-green.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-1.5+-red.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## Overview

This project demonstrates the complete data science pipeline from raw, messy Indian market data to actionable business insights.

### What It Does:
- Scrapes 1,500+ used car listings from OLX India using Selenium
- Cleans messy real-world data (missing values, outliers, duplicates)
- Engineers features: car age, price per km, brand dummies, city clusters
- Trains 7 machine learning models with hyperparameter tuning
- Interprets predictions using SHAP waterfall plots
- Identifies which car segments have the highest dealer markup

---

## Data Collection Process

### How the Data Was Collected

Instead of using a ready-made dataset, built a custom web scraper to collect real, messy, Indian-market used car data directly from OLX India.

### Why I Chose This Approach

- Real-World Data: OLX India has 300,000+ active car listings with complete details
- Messy & Unstructured: Perfect for practicing real-world data cleaning
- Indian Market Context: Captures unique pricing patterns, brands, and consumer behavior
- No Pre-Made Dataset: Demonstrates the complete data science workflow from scratch

### Scraping Strategy

1. Used Selenium for browser automation to handle dynamic content
2. Implemented random delays (2-5 seconds) between requests to be polite to the server
3. Scraped across 100+ pages using pagination (?page=1, ?page=2, ...)
4. Random sampling from each page to get diverse data
5. Extracted key fields: Price, Year, KM Driven, Fuel Type, Transmission, City, Title, Link
6. Saved progress every 50 cars to prevent data loss

### Data Collection Challenges

| Challenge | Solution |
|-----------|----------|
| Blocking/Timeouts | Used Selenium with proper headers and delays |
| Infinite Scroll | Used pagination instead of scrolling |
| Missing Values | Extracted year from title as fallback |
| Duplicate Listings | Removed duplicates using URL as unique identifier |
| Price Format | Used regex to extract numeric values from ₹ formats |

### Final Dataset

- Total Listings Scraped: 1,500+ cars
- Data Points per Listing: 9 fields
- Pages Scraped: 80+ pages
- Time Taken: ~9 hours 

### Sample Data Preview

| Title | Company | Price | Year | KM Driven | Fuel | Transmission | City |
|-------|---------|-------|------|-----------|------|--------------|------|
| Maruti Suzuki Baleno (2018) | Maruti Suzuki | ₹5,00,000 | 2018 | 90,000 | Petrol | Automatic | Delhi |
| Hyundai Creta (2021) | Hyundai | ₹7,80,000 | 2021 | 28,000 | Diesel | Automatic | Mumbai |
| Toyota Innova (2013) | Toyota | ₹6,49,999 | 2013 | 1,55,000 | Diesel | Automatic | Rajahmundry |


## Models Compared

| # | Model | Test R² | Accuracy |
|---|-------|---------|----------|
| 1 | Linear Regression | 0.40 | 40% |
| 2 | Ridge Regression | 0.41 | 41% |
| 3 | Lasso Regression | 0.39 | 39% |
| 4 | Decision Tree | 0.32 | 32% |
| 5 | Random Forest | 0.45 | 45% |
| 6 | XGBoost | 0.72 | 72% 🏆 |
| 7 | KNN | 0.50 | 50% |

### Best Model: XGBoost
- Test R²: 0.72 (72%)
- RMSE: 0.52
- MAE: 0.41

## Business Insights

### For Buyers:
- Cars aged 3-5 years offer the best value for money
- Maruti Suzuki and Hyundai have highest resale value
- Diesel cars in metro cities have better resale value

### For Sellers:
- Price based on age, brand, and km driven
- Metro cities command higher prices
- Automatic transmission adds premium

##  Future Work

- [ ] Deploy model as web app (Flask/Streamlit)
- [ ] Add real-time price prediction API
- [ ] Include more features (service history, ownership, insurance)
- [ ] Expand to other platforms (CarDekho, Cars24)
- [ ] Create interactive dashboard (Power BI/Tableau)
