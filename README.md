```markdown
# 🌍 AQI Intelligence Dashboard

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/)
[![Python 3.9](https://img.shields.io/badge/python-3.9-blue.svg)](https://www.python.org/downloads/release/python-390/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

An advanced, real-time Air Quality Monitoring and Forecasting system powered by Machine Learning. Designed for Karachi, Pakistan, this dashboard provides live AQI updates, 72-hour predictive forecasting, and health recommendations using XGBoost, LightGBM, and Scikit-Learn models.

---

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [Model Training](#model-training)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)
- [License & Author](#license--author)

---

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

## 💻 Installation & Setup

Follow these steps to get the project running on your local machine.

### 1. Clone the Repository
```bash
git clone https://github.com/hassaan217/10pearlstreamlit.git
cd 10pearlstreamlit
```

### 2. Create Virtual Environment
Create a virtual environment to isolate project dependencies.

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies
Install the required Python packages using the `requirements.txt` file.
```bash
pip install -r requirements.txt
```

### 4. Run the Application
Launch the Streamlit app.
```bash
streamlit run app.py
```
The application will open automatically in your default web browser at `http://localhost:8501`.

---

## ⚙️ Configuration

The application requires environment variables to connect to external services.

### Option A: Using `.env` file (Local)
Create a file named `.env` in the root directory and add the following:

```env
# MongoDB Connection String
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/?retryWrites=true&w=majority

# OpenWeather API Key
OPENWEATHER_API_KEY=your_api_key_here

# Geographic Coordinates (Karachi, Pakistan)
LATITUDE=24.8607
LONGITUDE=67.0011
```

### Option B: Using Streamlit Secrets (Cloud)
If deploying to Streamlit Cloud, go to your app settings > **Secrets** and paste the following in TOML format:

```toml
[database]
mongo_uri = "mongodb+srv://<username>:<password>@cluster.mongodb.net/?retryWrites=true&w=majority"

[weather]
api_key = "your_api_key_here"
latitude = 24.8607
longitude = 67.0011
```

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

## 🚢 Deployment

### Option A: Streamlit Cloud (Recommended)
1. Push your code to a GitHub repository.
2. Log in to [share.streamlit.io](https://share.streamlit.io).
3. Click **"New app"** and select your repository.
4. Ensure the main file path is `app.py`.
5. Paste your secrets in the **Secrets** tab.

### Option B: Docker
You can containerize the application using the following Dockerfile:

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8501

CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

Build and run:
```bash
docker build -t aqi-dashboard .
docker run -p 8501:8501 --env-file .env aqi-dashboard
```

---

## 🐛 Troubleshooting

### Error: `Permission denied to github-actions[bot]`
**Description:**
The GitHub Action fails to push model updates (`.pkl` files) back to the repository.
```
remote: Permission to hassaan217/10pearlstreamlit.git denied to github-actions[bot].
fatal: unable to access 'https://github.com/...': The requested URL returned error: 403
```
**Solution:**
1. Go to your GitHub Repository.
2. Navigate to **Settings** > **Actions** > **General**.
3. Scroll to **Workflow permissions**.
4. Select **Read and write permissions**.
5. Click **Save**.

### Error: `MongoDB Connection Timeout`
**Description:**
Cannot connect to the database.
**Solution:**
- Verify your IP is whitelisted in MongoDB Atlas (Network Access).
- Check if `MONGO_URI` is correct and contains `retryWrites=true&w=majority`.

### Error: `401 Unauthorized` (OpenWeather)
**Description:**
The API key is invalid.
**Solution:**
- Confirm the API key is correct.
- Note that new OpenWeather API keys may take 10-60 minutes to activate.

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
