# META-Stock-Market-Prediction
Stock market analysis and next-day price movement prediction for META using Python, yfinance, technical indicators, and Random Forest.
# 📈 META Stock Market Prediction Using Python

A Python-based stock market analysis and prediction project using **Yahoo Finance data** and a **Random Forest Classification model**. The project focuses on **Meta Platforms, Inc. (META)** and uses historical stock prices and technical indicators to predict the direction of the next day's closing price.

---

## 📌 Project Overview

This project demonstrates how Python can be used to collect, analyze, and model historical stock market data.

The notebook uses the `yfinance` library to retrieve financial information for **Meta Platforms (META)** from Yahoo Finance. It then explores company information, financial metrics, historical prices, and selected technical indicators.

A **Random Forest Classifier** is trained using historical market data to classify the next trading day's movement as:

* **UP (1)** – Tomorrow's closing price is higher than today's closing price.
* **DOWN (0)** – Tomorrow's closing price is lower than or equal to today's closing price.

> **Note:** This project is intended for educational and analytical purposes. The prediction output should not be considered financial or investment advice.

---

## 🎯 Objectives

The main objectives of this project are:

1. Retrieve financial information for Meta Platforms using Yahoo Finance.
2. Explore company-level financial metrics.
3. Collect historical META stock price data.
4. Analyze historical stock prices for a selected time period.
5. Calculate technical indicators such as:

   * 5-day Moving Average
   * 20-day Moving Average
   * Daily Return
6. Create a target variable representing the next day's price movement.
7. Train a Random Forest Classification model.
8. Evaluate the model using accuracy and a classification report.
9. Generate a prediction for the latest available observation.

---

## 🛠️ Technologies Used

| Technology                      | Purpose                        |
| ------------------------------- | ------------------------------ |
| Python                          | Programming language           |
| yfinance                        | Retrieving Yahoo Finance data  |
| Pandas                          | Data manipulation and analysis |
| NumPy                           | Numerical operations           |
| Scikit-learn                    | Machine learning               |
| Random Forest                   | Classification model           |
| Jupyter Notebook / Google Colab | Development environment        |

---

## 📂 Project Structure

```text
META-Stock-Prediction/
│
├── Finance.ipynb
└── README.md
```

### `Finance.ipynb`

The Jupyter Notebook contains the complete implementation, including:

* Installation of required libraries
* META company information
* Financial metrics
* Key-value financial information
* Historical stock data
* Period-specific historical data
* Technical indicator calculation
* Machine learning model training
* Model evaluation
* Next market movement prediction

---

## 📊 Data Source

The project retrieves financial and historical market data using:

**Yahoo Finance**

The ticker symbol used in the notebook is:

```text
META
```

which represents **Meta Platforms, Inc.**

The historical data includes market variables such as:

* Open
* High
* Low
* Close
* Volume
* Dividends
* Stock Splits

---

## 🔍 Financial Information Analysis

The notebook first retrieves company information using:

```python
import yfinance as yf

meta = yf.Ticker("META")

print(meta.info)
```

It also extracts selected financial metrics such as:

```python
print("Company Sector:", meta.info['sector'])
print("P/E Ratio:", meta.info['trailingPE'])
print("Company Beta:", meta.info['beta'])
```

This provides basic information about the company and selected market/financial indicators.

---

## 📈 Historical Stock Data

The project retrieves the complete available historical dataset using:

```python
data = meta.history(period="max")
```

The notebook also demonstrates how to retrieve data for a specific period.

The selected period in the notebook is:

```text
31 May 2019 – 30 January 2021
```

using:

```python
start_date = datetime.datetime(2019, 5, 31)
end_date = datetime.datetime(2021, 1, 30)

data = meta.history(
    start=start_date,
    end=end_date
)
```

---

## 📐 Feature Engineering

Before training the machine learning model, several features are created.

### 5-Day Moving Average

```python
df["MA_5"] = df["Close"].rolling(5).mean()
```

This calculates the average closing price over the previous five trading sessions.

### 20-Day Moving Average

```python
df["MA_20"] = df["Close"].rolling(20).mean()
```

This calculates the average closing price over the previous twenty trading sessions.

### Daily Return

```python
df["Return"] = df["Close"].pct_change()
```

This measures the percentage change in the closing price from one trading day to the next.

---

## 🎯 Target Variable

The project predicts the direction of the following day's closing price.

First, the next day's closing price is created:

```python
df["Tomorrow_Close"] = df["Close"].shift(-1)
```

The target variable is then created:

```python
df["Target"] = (
    df["Tomorrow_Close"] > df["Close"]
).astype(int)
```

The interpretation is:

| Target | Meaning                                    |
| -----: | ------------------------------------------ |
|    `1` | Next day's closing price is higher         |
|    `0` | Next day's closing price is lower or equal |

Rows containing missing values are removed before model training.

---

## 🤖 Machine Learning Model

The project uses a **Random Forest Classifier** from Scikit-learn.

The model uses the following features:

```text
Open
High
Low
Close
Volume
MA_5
MA_20
Return
```

The dataset is divided chronologically into:

* **80% Training Data**
* **20% Testing Data**

The model is initialized as:

```python
model = RandomForestClassifier(
    n_estimators=100,
    random_state=42
)
```

The model is then trained using:

```python
model.fit(X_train, y_train)
```

---

## 📏 Model Evaluation

The trained model generates predictions for the test dataset:

```python
predictions = model.predict(X_test)
```

Accuracy is calculated using:

```python
accuracy = accuracy_score(
    y_test,
    predictions
)
```

The notebook also generates a classification report containing metrics such as:

* Precision
* Recall
* F1-score
* Support

Example output format:

```text
Model Accuracy: XX.XX %

Classification Report:
              precision    recall    f1-score    support
...
```

The actual result may change when the notebook is executed again because Yahoo Finance data can change over time.

---

## 🔮 Market Movement Prediction

After training the model, the latest available feature row is used:

```python
latest = X.iloc[[-1]]
```

The model predicts the next market direction:

```python
prediction = model.predict(latest)[0]
```

The prediction is displayed as either:

```text
Predicted Movement: UP
```

or:

```text
Predicted Movement: DOWN
```

The notebook also displays the model's predicted class probabilities:

```text
Probability of DOWN: XX.XX %
Probability of UP: XX.XX %
```

---

## 🚀 How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/your-username/META-Stock-Prediction.git
```

### 2. Open the project

Navigate to the project directory:

```bash
cd META-Stock-Prediction
```

### 3. Install the required libraries

```bash
pip install yfinance pandas scikit-learn
```

The notebook also contains:

```python
!pip install yfinance
```

if you are working in Google Colab.

### 4. Open the notebook

You can open:

```text
Finance.ipynb
```

using:

* Jupyter Notebook
* JupyterLab
* Google Colab
* VS Code

### 5. Run the cells

Run the notebook cells from top to bottom.

---

## 🔄 Project Workflow

```text
Yahoo Finance
      ↓
META Financial Data
      ↓
Historical Stock Data
      ↓
Data Preparation
      ↓
Technical Indicators
      ↓
Feature Engineering
      ↓
Target Creation
      ↓
Train/Test Split
      ↓
Random Forest Classifier
      ↓
Model Evaluation
      ↓
Next Movement Prediction
```

---

## 📌 Features Used by the Model

| Feature | Description                              |
| ------- | ---------------------------------------- |
| Open    | Opening stock price                      |
| High    | Highest price during the trading session |
| Low     | Lowest price during the trading session  |
| Close   | Closing stock price                      |
| Volume  | Number of shares traded                  |
| MA_5    | 5-day moving average                     |
| MA_20   | 20-day moving average                    |
| Return  | Daily percentage return                  |

---

## ⚠️ Limitations

This project has several limitations:

* Stock prices are influenced by many factors that are not included in the model.
* The model uses a relatively limited set of technical features.
* Historical patterns do not necessarily continue in the future.
* Market conditions can change rapidly.
* The model predicts price direction rather than the exact future price.
* Yahoo Finance data and company information can change when the notebook is executed.
* Model accuracy alone does not determine whether a trading strategy would be profitable.

---

## 🔮 Future Improvements

The project can be extended by adding:

* More technical indicators such as RSI, MACD and Bollinger Bands.
* Additional market variables.
* Different machine learning algorithms.
* Hyperparameter tuning.
* Cross-validation designed for time-series data.
* More extensive feature engineering.
* Visualization of stock prices and technical indicators.
* Confusion matrix visualization.
* Feature importance analysis.
* Backtesting of a defined trading strategy.
* Comparison of different models.

Possible models for future comparison include:

```text
Logistic Regression
Random Forest
Gradient Boosting
XGBoost
Support Vector Machine
LSTM
```

---

## 📚 Learning Outcomes

Through this project, the following concepts are demonstrated:

* Financial data collection using Python
* Working with APIs/data libraries
* Data manipulation using Pandas
* Historical stock market analysis
* Technical indicator calculation
* Feature engineering
* Classification problems
* Random Forest machine learning
* Train/test splitting
* Model evaluation
* Prediction probabilities

---

## 👩‍💻 Author

**Vishakha Saini**

This project was created as a Python and machine learning project for exploring financial data analysis and stock market prediction.

---

## 📄 Disclaimer

This project is for **educational and demonstration purposes only**. It does not provide financial, investment, or trading advice. Predictions generated by the machine learning model should not be treated as recommendations to buy or sell securities.
