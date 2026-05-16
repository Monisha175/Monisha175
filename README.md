<!--
**Monisha175/Monisha175** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->


# AI-Powered Pest Disease Control System

> Machine learning system for predicting agricultural pest outbreaks — reducing chemical usage while sustaining crop health.

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat&logo=python)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110-009688?style=flat&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Scikit-learn](https://img.shields.io/badge/scikit--learn-1.4-F7931E?style=flat&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Overview

This system uses environmental and sensor data to predict pest outbreak risk before it occurs, enabling targeted — rather than blanket — pesticide application.

**Key outcomes:**
- 🔻 **30% reduction** in projected chemical usage
- 🎯 **87% F1-score** on pest risk classification (holdout test set)
- ⚡ **< 200ms** API response time for real-time IoT sensor queries

---

## How It Works

```
IoT Sensors (Temperature, Humidity, Soil pH, Rainfall)
        │
        ▼
  Data Ingestion API (FastAPI)
        │
  Preprocessing Pipeline
  (Imputation → Feature Engineering → Scaling)
        │
  Risk Classifier (Random Forest + XGBoost Ensemble)
        │
  Outbreak Risk Score (0.0 – 1.0) + Actionable Recommendation
        │
        ▼
  Farm Management Dashboard / Alert System
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.11 |
| API Framework | FastAPI |
| ML Models | Scikit-learn, XGBoost |
| Data Processing | Pandas, NumPy |
| Evaluation | MLflow (experiment tracking) |
| Deployment | Docker, uvicorn |

---

## Features

- **Ensemble model**: Random Forest + XGBoost voting classifier for robust predictions
- **Automated feature engineering**: Rolling averages, humidity-temperature interaction terms, seasonal encodings
- **REST API**: Real-time prediction endpoint for IoT device integration
- **Evaluation pipeline**: Automated cross-validation, confusion matrix, feature importance reports
- **Model versioning**: MLflow-tracked experiments for reproducible results

---

## Getting Started

### Prerequisites

```bash
python 3.11+
pip
```

### Installation

```bash
git clone https://github.com/Monisha175/ai-pest-control.git
cd ai-pest-control

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install -r requirements.txt
```

### Train the Model

```bash
python src/train.py --data data/sample_sensor_data.csv --output models/
```

### Run the API

```bash
uvicorn src.api.main:app --reload --port 8000
```

API docs auto-available at `http://localhost:8000/docs`

### Run with Docker

```bash
docker-compose up --build
```

---

## API Reference

### `POST /predict`

Predict pest outbreak risk from sensor readings.

**Request:**

```json
{
  "temperature_celsius": 28.5,
  "humidity_percent": 82.0,
  "soil_ph": 6.3,
  "rainfall_mm_last_7d": 45.2,
  "crop_type": "rice",
  "region": "south_india"
}
```

**Response:**

```json
{
  "risk_score": 0.74,
  "risk_level": "HIGH",
  "top_contributing_factors": [
    "humidity_percent",
    "temperature_celsius",
    "rainfall_mm_last_7d"
  ],
  "recommendation": "Apply targeted treatment within 48 hours. Focus on field zones with humidity > 80%.",
  "model_version": "v1.2.0",
  "inference_time_ms": 143
}
```

### `GET /health`

Returns API health status and model metadata.

### `GET /features/importance`

Returns feature importance rankings from the current model.

---

## Project Structure

```
ai-pest-control/
├── data/
│   └── sample_sensor_data.csv    # Sample dataset (anonymized)
├── models/                        # Saved model artifacts
├── notebooks/
│   └── eda.ipynb                 # Exploratory data analysis
├── src/
│   ├── api/
│   │   └── main.py               # FastAPI application
│   ├── model/
│   │   ├── train.py              # Training pipeline
│   │   ├── predict.py            # Inference logic
│   │   └── evaluate.py           # Evaluation metrics & reports
│   └── utils/
│       ├── preprocessing.py      # Feature engineering pipeline
│       └── config.py             # Configuration management
├── tests/
│   ├── test_api.py
│   └── test_model.py
├── Dockerfile
├── docker-compose.yml
└── requirements.txt
```

---

## Model Performance

| Metric | Value |
|---|---|
| Accuracy | 89.3% |
| F1 Score (weighted) | 87.1% |
| Precision | 88.5% |
| Recall | 85.9% |
| AUC-ROC | 0.93 |

*Evaluated on 20% stratified holdout set, 5-fold cross-validation.*

---

## Future Roadmap

- [ ] LSTM model for time-series outbreak pattern detection
- [ ] Satellite imagery integration (NDVI features)
- [ ] Multi-language support for farmer-facing alerts (Tamil, Hindi)
- [ ] Kafka integration for high-frequency IoT stream processing

---

## Author

**Monisha A** — [GitHub](https://github.com/Monisha175) · [LinkedIn](https://linkedin.com/)
