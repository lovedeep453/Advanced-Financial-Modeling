# Stock Performance Analysis & Forecasting

This project uses historical stock data to analyze, model, and forecast the short-term performance of twenty different stocks. By applying machine learning techniques, it identifies which stocks have the highest potential for next-day growth. The primary models used are **Linear Regression** and **Random Forest Regressor**, with the best model for each stock selected based on Mean Squared Error (MSE).

---

### Table of Contents
- [Project Goal](#project-goal)
- [Methodology](#methodology)
- [How to Use](#how-to-use)
- [Dependencies](#dependencies)
- [Results](#results)

---

### Project Goal
The main objective of this analysis is to create a data-driven pipeline that:
* Processes historical OHLC (Open, High, Low, Close) and Volume data for multiple stocks.
* Engineers relevant features for time-series forecasting, such as moving averages and lag features.
* Trains and evaluates two different regression models for each stock.
* Forecasts the next day's closing price.
* Ranks the stocks based on their forecasted percentage growth to identify top performers.

### Methodology
The project follows a systematic approach to ensure a robust analysis:

1.  **Data Loading & Preprocessing**: 
    * The initial dataset (`stock_data.csv`) is loaded into a pandas DataFrame. 
    * The `Date` column is converted to a datetime object to enable time-series analysis.

2.  **Feature Engineering**: 
    * To improve model accuracy, several new features are created from the historical data for each stock:
        * **Lag Features**: Closing prices from the previous 5 days (`lag_1` to `lag_5`).
        * **Moving Averages**: 5-day (`ma_5`) and 20-day (`ma_20`) moving averages to capture short and medium-term trends.
        * **Volatility**: The standard deviation of the closing price over a 5-day window, serving as a measure of market volatility.
    * The closing price of the next day (`target`) is set as the target variable for prediction.

3.  **Model Training**:
    * The data for each stock is split using `TimeSeriesSplit` to ensure the model trains on past data and is tested on recent data, respecting the temporal nature of the dataset.
    * Two models are trained:
        * **Linear Regression**: A simple and fast baseline model.
        * **Random Forest Regressor**: A more complex, ensemble model that can capture non-linear relationships.

4.  **Evaluation and Forecasting**:
    * For each stock, both models are evaluated based on their **Mean Squared Error (MSE)** on the test set.
    * The model with the lower MSE is selected as the "best model" for that stock.
    * This best model is then used to forecast the next day's closing price based on the most recent data.

5.  **Ranking**:
    * The forecasted closing price is used to calculate the potential percentage growth from the last known closing price.
    * All stocks are then ranked in descending order based on this forecasted growth, providing a clear list of investment opportunities.

### How to Use
To run this analysis yourself, follow these steps:

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/lovedeep453/Advanced-Financial-Modeling.git](https://github.com/lovedeep453/Advanced-Financial-Modeling.git)
    cd Advanced-Financial-Modeling
    ```

2.  **Install Dependencies:**
    *Ensure you have the `requirements.txt` file in your directory.*
    ```bash
    pip install -r requirements.txt
    ```

3.  **Prepare the Data:**
    *Place your `stock_data.csv` file inside a `data/` folder in the main project directory.*

4.  **Run the Notebook:**
    *Open and run the `Stock-Performance-Analysis/Stock_Performance_Analysis.ipynb` notebook in a Jupyter environment.* The cells will execute the full pipeline from data loading to final ranking.

### Dependencies
This project requires the following Python libraries:
* `pandas`
* `numpy`
* `scikit-learn`
* `matplotlib`
* `seaborn`

You can install all of them at once by running `pip install -r requirements.txt`.

### Results
The final output of the notebook is a ranked table and a corresponding bar chart that displays the forecasted next-day growth potential for each stock. The table clearly lists each stock's ticker, its last closing price, the best-performing model, and the calculated growth percentage. The bar chart provides a quick visual comparison, making it easy to identify the stocks with the highest and lowest predicted growth.

Based on the analysis, stocks like **STCKI** and **STCKN** showed the highest potential for short-term growth, while stocks such as **STCKQ** and **STCKK** were forecasted to have a negative performance. This ranking provides actionable insights for making informed, data-driven trading decisions.
