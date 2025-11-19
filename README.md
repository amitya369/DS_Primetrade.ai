# DS_Primetrade.ai
# 🚀 Trader Behavior Insights – Market Sentiment & Performance Analysis  
### *Junior Data Scientist Assignment – Bajarangs / PrimeTrade*

This project explores how **market sentiment (Fear–Greed Index)** influences **trader performance** on the Hyperliquid platform.  
Using over **211k historical trades** and **2,600+ days of sentiment data**, the analysis demonstrates how emotional market regimes affect profitability and how **sentiment momentum** improves predictive modeling.

---

## 📁 Project Structure
├── data/
│ ├── historical_data.csv
│ ├── fear_greed_index.csv
│
├── notebooks/
│ ├── Trader_Insights_Analysis.ipynb
│
├── outputs/
│ ├── pnl_boxplot.png
│ ├── feature_importance.png
│ ├── feature_importance_v2.png
│ ├── model_metrics.json
│
├── README.md
└── requirements.txt

---

# 📘 1. Overview

This project examines the relationship between:

- **Market Sentiment** – Bitcoin Fear & Greed Index  
- **Trader Performance** – Hyperliquid's historical trade execution data  

The goal is to uncover **behavioral patterns**, quantify differences in outcomes across sentiment regimes, and build predictive models capable of forecasting trade success.

---

# 📊 2. Datasets Used

### **2.1 Bitcoin Fear & Greed Index**
- 2,644 daily entries  
- Columns: `timestamp`, `value`, `classification`, `date`  
- Standardized to: **Fear**, **Neutral**, **Greed**

### **2.2 Hyperliquid Historical Trade Data**
- 211,224 trades  
- Columns include: execution price, size, side, pnl, timestamps, etc.

---

# 🛠️ 3. Data Preparation

### ✔ Converted timestamps to proper datetime formats  
### ✔ Created `trade_date` to match sentiment  
### ✔ Cleaned numeric fields (price, size, PnL)  
### ✔ Computed notional value (USD exposure)  
### ✔ Encoded trade direction (BUY = 1, SELL = 0)  
### ✔ Merged sentiment → each trade via date mapping  
### ✔ Engineered lagged sentiment features:
- `sentiment_num_lag1`
- `sentiment_num_lag7` (7-day rolling average)

**Sentiment momentum became one of the strongest predictors.**

---

# 📈 4. Exploratory Data Analysis

## **PnL Summary by Sentiment**

| Sentiment | Trades | Mean PnL | Median PnL | Win Rate |
|----------|--------|----------|-------------|-----------|
| **Greed** | 90,301 | 54.35 | 0.0 | 42.0% |
| **Fear** | 83,237 | 49.21 | 0.0 | 40.8% |
| **Neutral** | 37,686 | 34.30 | 0.0 | 39.7% |

### 💡 Key Insight:
> **Profitability is highest during Greed markets and lowest during Neutral markets.**

---

# 🧪 5. Statistical Testing

## **Mann–Whitney U Test → p = 0.00087**
✔ Statistically significant difference between **Fear vs Greed** performance  
✔ Confirms traders behave differently in optimistic vs fearful markets

## **T-test → Not significant**  
Expected due to **non-normal heavy-tailed PnL distribution**.

---

# 🤖 6. Predictive Modeling

### **6.1 Baseline Random Forest**
- Accuracy: **75.0%**
- ROC-AUC: **0.83**

### **6.2 Improved Random Forest (with sentiment momentum)**
- Accuracy: **81.47%**
- ROC-AUC: **0.893**

📈 **+6.5% Accuracy Boost Using Lag Features**  
📈 **Stronger classification of win/loss trades**

---

# 🔍 7. Feature Importance (Improved Model)

| Feature | Importance |
|---------|------------|
| Execution price | **0.389** |
| Side (Buy/Sell) | **0.225** |
| Size tokens | 0.100 |
| Sentiment trend (7-day) | **0.084** |
| Day of week | 0.070 |
| Notional | 0.070 |
| Lag-1 sentiment | 0.033 |
| Current sentiment | 0.028 |

### 💡 Insight:
> **Sentiment trend is more predictive than raw sentiment.**

---

# 📂 8. Visualizations

Located in: `/outputs/`

- `pnl_boxplot.png` — PnL distribution vs sentiment  
- `feature_importance.png` — Baseline model  
- `feature_importance_v2.png` — Improved model with lag features  

---

# 🏁 9. Conclusion

- Traders perform **significantly better in Greed markets**.  
- Neutral sentiment produces the **weakest profitability**.  
- **Lagged sentiment** improves predictive modeling significantly.  
- Final model achieves:  
  - **Accuracy: 81.47%**  
  - **ROC-AUC: 0.893**  
- Sentiment momentum is a **valuable trading signal** for strategy design.

This project demonstrates how sentiment-driven analytics can enhance trading intelligence in Web3 environments.

---

# 📬 10. How to Run

```bash
pip install -r requirements.txt
-notebooks/Trader_Insights_Analysis.ipynb

