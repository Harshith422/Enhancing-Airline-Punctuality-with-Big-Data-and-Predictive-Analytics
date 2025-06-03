# ✈️ Enhancing Airline Punctuality with Big Data and Predictive Analytics

A scalable machine learning system to predict airline delays using **PySpark**, **Gradient Boosted Trees**, and **AWS S3**, with a **Flask web interface** for real-time predictions.

---

## 📌 Overview

Flight delays cost airlines money, frustrate passengers, and disrupt operations. This project uses historical flight, weather, and air traffic data to:

- Predict flight delays
- Identify the most likely causes (carrier, weather, NAS, late aircraft)
- Provide delay probabilities via a user-friendly web interface

---

## 🎯 Objectives

- Predict whether a flight will be delayed using machine learning
- Use Big Data tools (Apache Spark) for scalable data processing
- Analyze delay causes: carrier, weather, NAS, late aircraft
- Provide real-time predictions using a Flask web application
- Store and manage data/models using AWS S3

---

## 🛠️ Technologies Used

- **PySpark** – Distributed data processing
- **Spark MLlib** – Machine learning pipeline
- **GBTClassifier** – Gradient Boosted Trees model
- **Flask** – Web interface
- **AWS S3** – Storage for datasets and models

---

## 📂 Dataset

**Source**: [Bureau of Transportation Statistics](https://www.bts.gov)

- `Airline_Delay_Cause.csv`: Historical flight data including:
  - `arr_flights`, `arr_del15`
  - `carrier_ct`, `weather_ct`, `nas_ct`, `late_aircraft_ct`
  - `carrier`, `airport`, `year`, `month`
- `historical_estimates.json`: Backup stats for real-time inference

---

## ⚙️ Feature Engineering

- **Temporal Features**: `month_sin`, `month_cos` for seasonal effects
- **Categorical Encoding**: Indexed carrier and airport codes
- **Interaction Terms**: Airline-airport pairings (e.g., DL_ATL)
- **Proportions**: Cause-based ratios (e.g., `carrier_prop`)
- **Standardization**: `arr_flights_scaled` for stable training

---

## 🤖 Model Details

- **Model**: `GBTClassifier` from Spark MLlib
- **Task**: Binary classification (delayed or not)
- **Split**: 80% training / 20% testing
- **Threshold**: Delay if `P(delay=1) > 0.65`
- **Accuracy**: ~85%
- **Precision**: ~80%
- **Recall**: ~88%

---

## 🧪 Example Predictions

| Airport | Airline | Date        | Delay Probability | Status     | Likely Cause     |
|---------|---------|-------------|-------------------|------------|------------------|
| LAX     | B6      | Apr 11, 2025| 12%               | On-Time    | —                |
| LAS     | UA      | Jun 24, 2024| 83%               | Delayed    | Weather (36%)    |

---
## 🖥️ Web Application

Built using Flask:

- Input: Airline, Airport, Month, Year
- Output: Delay prediction with probability and cause
- Backend uses pre-trained PySpark GBT model
- Deployed locally (`http://localhost:5000`) or optionally to the cloud

---

## 📦 AWS S3 Integration

- **Input**: Flight datasets stored in `s3a://` buckets
- **Output**: Trained models, prediction logs, and statistics
- **Configured via**: `spark.hadoop.fs.s3a.access.key` and `secret.key`

---

## 👨‍💻 Contributors
**Guide**: Dr. Chitra P, Amrita Vishwa Vidyapeetham

---

## 🚀 Future Enhancements

- Real-time FAA and weather data integration  
- Day-level prediction granularity  
- Advanced models (LSTM, XGBoost)  
- Deployment to cloud (AWS/GCP/Azure)  
- Alerts via email/SMS on high delay risk

---

## 📜 License

This project is for academic purposes only.  
Dataset is public from the U.S. Department of Transportation [BTS.gov](https://www.bts.gov).
