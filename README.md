Stock Performance Analysis & Forecasting
This project uses historical stock data to analyze, model, and forecast the short-term performance of twenty different stocks. By applying machine learning techniques, it identifies which stocks have the highest potential for next-day growth.
The primary models used for prediction are Linear Regression and Random Forest Regressor. The pipeline evaluates both models for each stock and selects the one with the lower Mean Squared Error (MSE) to make the final forecast.
Table of Contents
* Project Goal
* Methodology
* How to Use
* Dependencies
* Results
Project Goal
The main objective of this analysis is to create a data-driven pipeline that:
1. Processes historical OHLC (Open, High, Low, Close) and Volume data for multiple stocks.
2. Engineers relevant features for time-series forecasting, such as moving averages and lag features.
3. Trains and evaluates two different regression models for each stock.
4. Forecasts the next day's closing price.
5. Ranks the stocks based on their forecasted percentage growth to identify the top performers.
Methodology
The project follows a systematic approach to ensure a robust analysis:
1. Data Loading & Preprocessing: The initial dataset (stock_data.csv) is loaded into a pandas DataFrame. The Date column is converted to a datetime object to enable time-series analysis.
2. Feature Engineering: To improve model accuracy, several new features are created from the historical data for each stock:
   * Lag Features: Closing prices from the previous 5 days (lag_1 to lag_5).
   * Moving Averages: 5-day (ma_5) and 20-day (ma_20) moving averages to capture short and medium-term trends.
   * Volatility: The standard deviation of the closing price over a 5-day window, serving as a measure of market volatility.
   * Target Variable: The closing price of the next day (target), which is what the models aim to predict.
3. Model Training:
   * The data for each stock is split using TimeSeriesSplit to ensure that the model trains on past data and is tested on more recent data, which respects the temporal nature of the dataset.
   * Two models are trained:
      * Linear Regression: A simple and fast baseline model.
      * Random Forest Regressor: A more complex, ensemble model that can capture non-linear relationships.
   * The models are trained on the engineered features to predict the target variable.
4. Evaluation and Forecasting:
   * For each stock, both models are evaluated based on their Mean Squared Error (MSE) on the test set.
   * The model with the lower MSE is selected as the "best model" for that particular stock.
   * This best model is then used to forecast the next day's closing price based on the most recent available data.
5. Ranking:
   * The forecasted closing price is used to calculate the potential percentage growth from the last known closing price.
   * All stocks are then ranked in descending order based on this forecasted growth, providing a clear list of investment opportunities.
How to Use
To run this analysis yourself, follow these steps:
1. Clone the Repository:
git clone [https://your-repository-url.git](https://your-repository-url.git)
cd your-repository-directory


2. Install Dependencies: Ensure you have all the required libraries installed. You can do this using pip:
pip install -r requirements.txt


(Note: You may need to create a requirements.txt file from the dependencies listed below).
3. Prepare the Data: Make sure your stock_data.csv file is located in a ../data/ directory relative to the notebook, or update the path in the data loading cell.
4. Run the Notebook: Open and run the Stock_Performance_Analysis.ipynb notebook in a Jupyter environment. The cells are organized sequentially and will execute the full pipeline from data loading to final ranking.
Dependencies
This project requires the following Python libraries:
   * pandas
   * numpy
   * scikit-learn
   * matplotlib
   * seaborn
You can install them via pip:
pip install pandas numpy scikit-learn matplotlib seaborn


Results
The final output of the notebook is a ranked table and a corresponding bar chart that displays the forecasted next-day growth potential for each stock.
   * The table clearly lists each stock's ticker, its last closing price, the best-performing model for its forecast, and the calculated growth percentage.
   * The bar chart provides a quick visual comparison, making it easy to identify the stocks with the highest and lowest predicted growth.
Based on the analysis, stocks like STCKI and STCKN showed the highest potential for short-term growth, while stocks such as STCKQ and STCKK were forecasted to have a negative performance. This ranking provides actionable insights for making informed, data-driven trading decisions.
