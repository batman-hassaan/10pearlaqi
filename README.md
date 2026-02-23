
# 🌍 AQI Intelligence Dashboard

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/)
[![Python 3.9](https://img.shields.io/badge/python-3.9-blue.svg)](https://www.python.org/downloads/release/python-390/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

An advanced, real-time Air Quality Monitoring and Forecasting system powered by Machine Learning. Designed for Karachi, Pakistan, this dashboard provides live AQI updates, 72-hour predictive forecasting, and health recommendations using XGBoost, LightGBM, and Scikit-Learn models.

### Preview Live link
https://10pearlapp-7btibmslyera2uqrvugxwj.streamlit.app/

### StreamLit Github deployment
https://github.com/hassaan217/10pearlstreamlit


## 🚀 Project Overview

The **AQI Intelligence Dashboard** is a comprehensive full-stack data application that ingests real-time weather and pollution data, processes it through machine learning pipelines, and visualizes insights via an interactive web interface.

### Core Objectives
- **Real-time Monitoring**: Track PM2.5, PM10, NO2, and other pollutants live.
- **Predictive Analytics**: Forecast air quality for the next 72 hours using ensemble models.
- **Health Advisory**: Provide actionable health advice based on current AQI levels.
- **Model Comparison**: Visualize performance metrics (R², RMSE, MAE) across multiple algorithms.

---

## ✨ Key Features

- **🔴 Live AQI Monitoring**: Real-time gauge charts with dynamic color coding (Good to Severe).
- **🤖 Machine Learning Integration**: 
  - XGBoost Regressor
  - LightGBM Regressor
  - Random Forest
  - Histogram Gradient Boosting
- **📈 72-Hour Forecast**: Hourly and daily predictions with temperature overlays.
- **🏥 Health Recommendations**: Context-aware advice based on pollutant levels and weather.
- **💾 MongoDB Integration**: Secure, scalable storage for historical data and model artifacts.
- **🔄 Automated CI/CD**: GitHub Actions workflow for automated model retraining and deployment.
- **🌙 Dark Mode UI**: Modern, responsive Streamlit interface with custom CSS styling.

---

## 🛠️ Technology Stack

| Category | Technology | Version/Description | Purpose |
| :--- | :--- | :--- | :--- |
| **Frontend** | Streamlit | 1.28+ | Interactive Web Framework |
| | Plotly | 5.17+ | Interactive Charts & Graphs |
| **Backend** | Python | 3.9+ | Core Logic & Processing |
| | Pandas | 2.0+ | Data Manipulation |
| | NumPy | 1.24+ | Numerical Computing |
| **Database** | MongoDB | 6.0+ | NoSQL Data Storage |
| | PyMongo | 4.5+ | MongoDB Driver |
| **Machine Learning** | Scikit-learn | 1.3+ | ML Models & Metrics |
| | XGBoost | 2.0+ | Gradient Boosting |
| | LightGBM | 4.1+ | Light Gradient Boosting |
| | Joblib | 1.3+ | Model Serialization |
| **APIs** | OpenWeather API | Current | Real-time Weather Data |
| **DevOps** | GitHub Actions | - | CI/CD Pipeline |

---

## 🏗️ System Architecture

The system follows a modular pipeline architecture:

1.  **Data Ingestion Layer**:
    - Fetches real-time weather data from OpenWeather API.
    - Falls back to synthetic data generation if the API fails.
2.  **Storage Layer**:
    - Stores historical data in MongoDB (`raw_aqi` collection).
    - Persists trained models (`.pkl` files) in the repository.
3.  **Processing Layer**:
    - Feature Engineering (Time, Seasonality, Weather).
    - Standard Scaling for normalization.
    - Model Training & Evaluation.
4.  **Presentation Layer**:
    - Streamlit Dashboard.
    - Plotly Visualizations (Gauges, Line charts, Radar charts).

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.9 or higher**
- **Git**
- **MongoDB Atlas Account** (Free tier recommended)
- **OpenWeather API Key** (Free tier available)

---



---

## 📖 Usage Guide

### 1. Dashboard View
- Observe the **Current AQI** gauge.
- Check pollutant levels (PM2.5, PM10, NO2) in the metric cards.
- Use the **Auto-refresh** toggle in the sidebar for live updates.

### 2. Forecasting
- Scroll down to the **3-Day Forecast** section.
- View hourly AQI and temperature trends.
- Hover over charts to see specific data points.

### 3. Model Training
- Click **"🤖 Train Models"** in the sidebar.
- The system will train 4 models (XGBoost, LightGBM, RF, HistGB).
- Compare models using the **Radar Chart** and **Metrics Table**.
- Select the best performing model for predictions.

### 4. Data Collection
- Click **"🔄 Collect Data"** to manually trigger a data fetch.
- This retrieves current weather and calculates pollution estimates.

---

## 🧠 Model Training

The project utilizes an optimized training pipeline to ensure speed and accuracy.

### Algorithms Used
| Algorithm | Strength | Optimization |
| :--- | :--- | :--- |
| **XGBoost** | High accuracy, handles missing data | `n_estimators=50`, `max_depth=5` |
| **LightGBM** | Fast training, low memory usage | `n_estimators=50`, `max_depth=5` |
| **Random Forest** | Robust, reduces overfitting | `n_estimators=50` |
| **Hist Gradient Boosting** | Efficient for large datasets | `max_iter=50` |

### Metrics Tracked
- **R² Score**: Coefficient of Determination.
- **RMSE**: Root Mean Squared Error.
- **MAE**: Mean Absolute Error.
- **Latency**: Prediction time in milliseconds.

> **Note**: The models are optimized to train in seconds rather than minutes by reducing estimators and cross-validation folds, making it suitable for real-time retraining.

---

### Issue: Training is too slow
**Description:**
The training process takes several minutes.
**Solution:**
- Ensure you are using the optimized `train_models` function (as updated in the latest code).
- Verify `n_jobs=-1` is set in the model configurations to use all CPU cores.

---

## 📄 License & Author

**License:**  
This project is licensed under the MIT License.

**Author:**  
**Hassaan Ahmed**  
[GitHub Profile](https://github.com/hassaan217)

**Acknowledgments:**  
- [OpenWeatherMap](https://openweathermap.org/) for weather data.
- [Streamlit](https://streamlit.io/) for the web framework.
- [MongoDB](https://www.mongodb.com/) for database support.
```
