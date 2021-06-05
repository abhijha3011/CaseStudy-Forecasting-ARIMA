# CaseStudy-Forecasting-ARIMA
Time Series analysis on monthly "Sales" data. Here, we created a Time series model by using ARIMA and forecasted next 12 days sales amount.
# Data Set --> forecasting_data.xlsx.

It has the following columns:

amt: Amount spend on Logistics each month from May 2015 to Mar 2018
year.mon: A date column representing the month and year of the observation
log.amt: The logarithmic values of ‘amt’. This is the target variable
predicted: The fitted valued of a particular model, which also provides the forecast for 12 future periods ending in March 2019.
Lower CI: Lower confidence interval of prediction 
Upper CI: Upper confidence interval of predictions

# Software used: Python, Jupyter Notebook
Version: 3.8.3__
Packages/libraries used: Pandas(1.0.5),matplotlib(3.2.2),numpy(1.18.5),scipy(1.5)

# Model Used: 
ARMA. In fact, the AR and MA components are identical, combining a general 
autoregressive model AR(p) and general moving average model MA(q). AR(p) makes predictions using previous values 
of the dependent variable. MA(q) makes predictions using the series mean and previous errors.
An ARMA model is a stationary model; If your model isn’t stationary, then you can achieve stationarity by taking a series of differences. 
The “I” in the ARIMA model stands for integrated; It is a measure of how many non-seasonal 
differences are needed to achieve stationarity. If no differencing is involved in the model, then it becomes simply an ARMA.
After performing adfuller_test,we got to know our data was stationary so here we apply ARMA.

Used other modeling technique "STACKED LSTM", validation error was high so rejected that model for now. It was needed some optimization
In time series modelling, the predictions over time become less and less accurate and hence it is a more realistic 
approach to re-train the model with actual data as it gets available for further predictions. Since training of statistical 
models are not time consuming, walk-forward validation is the most preferred solution to get most accurate results.
# walk-forward validation
history = [x for x in train]

predictions = list()

for i in range(len(test)):

    yhat = history[-1]
    
    predictions.append(yhat)
    
# observation
    obs = test[i]
    
    history.append(obs)
    
    print('>Predicted=%.3f, Expected=%.3f' % (yhat, obs))
    
# report performance

rmse = sqrt(mean_squared_error(test, predictions))

print('RMSE: %.3f' % rmse)
