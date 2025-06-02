# 🔋 AI for Energy Efficiency – Enfield Hackathon 2025

## 👨‍💻 Team IU-UN 2025 (Internationl University - University of Nottingham)


| Name                            | Description                          |
|---------------------------------|--------------------------------------|
| Nguyen Trung Ky                 | Team Leader, Lecturer at IU          |
| Ly Gia Bao                      | IU student                           |
| Nguyen Thanh Nam                | IU student                           |
| Pham Thien Nhan                 | IU-UN student                        |
| Nguyen The Hao                  | IU student                           |
| Prof. Shreyank Narayana Gowda   | Lecturer at UN                       |
| Prof. Christian Wagner          | Lecturer at UN                       |

---

## 🧠 Introduction

![Enfield Hackathon](https://media.licdn.com/dms/image/v2/D4E22AQGOm6wkbsU31g/feedshare-shrink_800/B4EZWu.w87HcAg-/0/1742397444728?e=2147483647&v=beta&t=JkB6uE1oMxhVwyin8KqbcJewqK5K7eQcnuAizUnS89g)

This project was developed as part of the [Enfield Hackathon 2025: AI for Energy Efficiency](https://cis.ttu.ee/2025/03/01/enfield-hackathon-2025-ai-for-energy-efficiency/), hosted in Tallinn. Our team, **IU-UN 2025**, aimed to tackle the critical issue of energy consumption forecasting in urban environments. Accurate prediction of electricity usage supports greener energy practices by enabling:

- Reduced greenhouse gas emissions  
- Better air quality  
- Economic optimization  
- Sustainable energy planning  

The core of our solution is a machine learning pipeline utilizing **LSTM with Reinforcement Learning**, and **XGBoost** to predict energy consumption in different buildings using historical hourly usage data.

---

## 📈 Energy Usage Forecasting: 10-Month Prediction from 2-Month Input

This project forecasts **the next 10 months of hourly electricity usage** for a new building using **only the first 2 months of 2023** as input. It compares two modeling approaches:

- 🧠 **LSTM + Reinforcement Learning (RL)**  
- 🌲 **XGBoost Regressor**

---

## 🗂️ Project Structure

### 📁 Data Preprocessing

#### `preprocess.ipynb`
- Loads and cleans the main energy consumption dataset.

#### `preprocess_weather.ipynb`
- Loads and processes external weather datasets.

### 🗂️ Project Setup

Follow these instructions to set up and run the project locally.

#### 1. Clone the Repository
```bash
git clone https://github.com/baoly1309/Tallinn_Hackathon.git
cd Tallinn_Hackathon

```

#### 2. Create a Virtual Environment
Using venv:
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```
Or using conda
```bash
conda create -n tallinn_hackathon python=3.10
conda activate tallinn_hackathon
```
#### 3. Install dependencies
For LSTM Model:
```bash
pip install -r requirements_lstm.txt
```
For XGBoost Model:
```bash
pip install -r requirements_xgboost.txt
```
#### 4. Run the Models
Train and evaluate the LSTM model:
```bash
# For LSTM model
jupyter notebook lstm_rl.ipynb
```
Train and evaluate the XGBoost model:
```bash
# For XGBoost model
jupyter notebook xgboost_model.ipynb
```

---

### 📊 Exploratory Data Analysis

#### `eda.ipynb`
- Visualizes energy usage patterns.  
- Analyzes differences between buildings, time-of-day trends.

---

### 🧠 Model 1 – LSTM + Reinforcement Learning

#### `lstm_rl.ipynb`
- Builds an LSTM model.  
- Integrates Reinforcement Learning to improve long-term predictions.  
- Trained on the first 2 months of each building’s data and tested on the next 10 months.

> ⚠️ **Limitation:**  
> When applied to a new building with only 2 months of data, normalization was not possible. This led to **poor generalization** and **flat predictions**.

---

### 🛠️ Feature Engineering

#### `feature_engineering.ipynb`
- Constructs input features:  
  - Time encodings (hour, day, weekday, month) as sin/cos functions

---

### 🌲 Model 2 – XGBoost

#### `xgboost_model.ipynb`
- Trains an XGBoost regressor on the first 2 months and tests on the next 10 months of hourly usage.  
- Uses walk-forward prediction.  
- **No normalization required**, allowing better generalization to unseen buildings.

#### `submission_xgboost.ipynb`
- Generates final predictions.  
- Prepares submission file (CSV) for the new building.

---

## ✅ Why XGBoost

| Model               | Normalization Required | Handles New Building Easily | Forecast Quality |
|--------------------|------------------------|------------------------------|------------------|
| LSTM + RL          | ✅ Yes                 | ❌ Poor                      | ❌ Bad           |
| XGBoost Regressor  | ❌ No                  | ✅ Good                      | ✅ Strong        |

---

## 📉 MAPE Comparison: LSTM+RL vs XGBoost

### 🔁 LSTM + Reinforcement Learning (Before vs After Fine-Tuning)

| Building(s)                 | MAPE Before RL | MAPE After RL |
|----------------------------|----------------|----------------|
| ICT                        | 10.47%         | 10.83%         |
| U06, U06A, U05B            | 9.49%          | 8.97%          |
| OBS                        | 43.98%         | 44.79%         |
| U05, U04, U04B, GEO        | 14.92%         | 13.35%         |
| TEG                        | 56.78%         | 55.75%         |
| LIB                        | 25.09%         | 24.32%         |
| MEK                        | 27.37%         | 21.90%         |
| SOC                        | 32.29%         | 16.27%         |
| S01                        | 51.92%         | 48.80%         |
| D04                        | 23.27%         | 24.56%         |

---

### 🌲 XGBoost MAPE Results

| Building(s)                 | MAPE (XGBoost) |
|----------------------------|----------------|
| ICT                        | 9.40%          |
| U06, U06A, U05B            | 11.02%         |
| OBS                        | 235.23%        |
| U05, U04, U04B, GEO        | 11.97%         |
| TEG                        | ❗ 2.16e+17%    |
| LIB                        | 23.95%         |
| MEK                        | ❗ 7.57e+15%    |
| SOC                        | 33.82%         |
| S01                        | 277.91%        |
| D04                        | 61.01%         |

🔍 **Observation:**
Reinforcement Learning helped reduce error for some complex buildings, but XGBoost was more consistent overall.

![alt text](https://i.ibb.co/pBBKdjZk/sample-predict.png)
---

## 🏆 Final Submission Result

Only the **XGBoost** model was submitted for final evaluation.

- ✅ **Final MAPE on test building**: **7.95%**
- 🥉 **Ranked Top 3 Most Accurate Prediction** at Enfield Hackathon 2025!

### ❌ Why LSTM+RL Was Not Submitted

The LSTM+RL model failed on the final test building due to:

- Inability to normalize with only 2 months of data  
- Predicting a **flat line** (no variation)  

> 🔎 Final decision: **Only XGBoost predictions were submitted.**

---

## 🧾 Conclusion

In this project, we tried to forecast 10 months of electricity usage from just 2 months of data.

- **LSTM + RL** worked during training but couldn’t generalize to new buildings due to normalization issues.  
- **XGBoost** gave a much better result and was easier to apply.  

For future work, we plan to combine the strengths of both models or improve the preprocessing for LSTM.

---
