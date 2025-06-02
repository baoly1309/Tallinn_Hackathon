# AI for Energy Efficiency – Enfield Hackathon 2025

## 🔋 Introduction

This project was developed as part of the [Enfield Hackathon 2025: AI for Energy Efficiency](https://cis.ttu.ee/2025/03/01/enfield-hackathon-2025-ai-for-energy-efficiency/), hosted in Tallinn. Our team, **IU-UN 2025**, aimed to tackle the critical issue of energy consumption forecasting in urban environments. Accurate prediction of electricity usage supports greener energy practices by enabling:

- Reduced greenhouse gas emissions
- Better air quality
- Economic optimization
- Sustainable energy planning

The core of our solution is a machine learning pipeline utilizing **LSTM**, **Bidirectional LSTM**, **Reinforcement Learning**, and **XGBoost** to predict energy consumption in different buildings using historical hourly usage data.

---

## 📊 1. Data Preprocessing

The dataset consists of hourly electricity usage data for 10 building areas from January 2023 to January 2024. Each entry represents usage (in kWh) along with building metadata such as area (m²).

Preprocessing included:

- **Segmentation by building and time** for individualized modeling
- **Conversion of timestamps** to cyclical temporal features (e.g., hour of day, month)

---

## 🧩 2. Handling Missing Values

Missing values were addressed using:

- **Linear interpolation** for small gaps
- **Forward-filling** for terminal missing entries
- Validation to ensure temporal consistency and avoid data leakage

---

## ⚖️ 3. Normalization

Each feature was scaled using **Min-Max Normalization** to ensure consistency and numerical stability across time series inputs. This was particularly important for training deep learning models sensitive to scale.

---

## 🛠️ 4. Feature Engineering

Engineered features included:

- **Temporal patterns** (hour, day of week, month encoded with sine/cosine transforms)
- **Lag features** capturing recent consumption trends
- **Building metadata**, such as area in square meters, integrated into model inputs

These features allowed the models to capture both periodicity and contextual dependencies.

---

## 🔁 5. Building LSTM Model

A standard **Long Short-Term Memory (LSTM)** model was implemented to:

- Handle long-range dependencies
- Capture nonlinear relationships in electricity usage
- Model temporal dynamics efficiently

The LSTM accepted sequences of past 2 months of hourly data and forecasted the next 10 months.

---

## 🔁🔁 6. Building Bidirectional LSTM

To enhance performance, a **Bidirectional LSTM** (BiLSTM) was trained:

- Allows learning from both past and future temporal context
- Slight improvement in pattern recognition, especially for buildings with cyclical trends

Limitations included higher computational cost and overfitting risks in limited data scenarios.

---

## 🧠⚙️ 7. LSTM Fine-Tuning with Reinforcement Learning

We incorporated **Reinforcement Learning (RL)** to fine-tune the LSTM model:

- RL was used to minimize the prediction error (e.g., MAPE) by rewarding better predictions
- Helped break strong correlations in training states and improve generalization
- Significant reduction in forecast error observed after 5 episodes of fine-tuning

---

## 🌲 8. Building XGBoost Baseline

As a benchmark, we implemented an **XGBoost regressor**:

- Trained on flattened feature sets
- Faster to train and interpret
- Performed well in short-term prediction but underperformed on long horizons compared to LSTM

---

## ✅ 9. Testing and Validation

All models were evaluated using:

- **Mean Absolute Percentage Error (MAPE)** as the primary metric
- 10-fold cross-validation across buildings
- Comparison across models:
  - LSTM outperformed others in most buildings
  - RL fine-tuning improved generalization
  - XGBoost was fastest but less accurate for multi-month forecasts

---

## 🧠 10. Conclusion

Our project demonstrates that deep learning models—especially LSTM fine-tuned with reinforcement learning—can significantly enhance the accuracy of long-term electricity consumption forecasts. The solution is scalable across diverse building types and provides a foundation for data-informed energy efficiency planning.

---

## 👨‍💻 Team IU-UN 2025

- **Nguyen Trung Ky** (Team Leader)
- Ly Gia Bao  
- Nguyen Thanh Nam  
- **Pham Thien Nhan**  
- Nguyen The Hao  
- Prof. Shreyank Narayana Gowda (University of Nottingham)  
- Prof. Christian Wagner (University of Nottingham)  

---
