# retail_giant_case_study
Forecast the sales of products for the next 6 months to have a proper estimate of the inventory. This will also help in planning business processes ahead of time. 

### Business Problem 
Global Mart is an online supergiant store that has worldwide operations. This store takes orders and delivers across the globe and deals with all the major product categories — consumer, corporate & home office. As part of the analytics team the objective is to forecast the sales of products using historic timeseries data to aid in inventory management and business processes for a client. 

 The dataset has the following 5 attributes:
                                                                Attributes	Description
                                                                Order-Date	The date on which the order was placed
                                                                Segment	    The segment to which the product belongs
                                                                Market	    The market to which the customer belongs
                                                                Sales	      Total sales value of the transaction
                                                                Profit	    Profit made on the transaction
                                                                
The store caters to 7 different geographical market segments and 3 major customer segments, i.e. consumer, corporate and home as can be seen in the table below.

                                                                Market	        ``        Segment
                                                                Africa	                  Consumer
                                                                APAC (Asia Pacific)	      Corporate
                                                                Canada	                  Home Office
                                                                EMEA(Middle East)	 
                                                                EU (European Union)	 
                                                                LATAM (Latin America)	 
                                                                US (United States)	 
Based on these, there are 21 unique "Market-Segments" for which the sales forecasts can be made. That is the dataset needs to be prepared such that I get the Order-Date, Sales and Profit for the 21 market segments.
Now, due to certain unpredictable circumstances in the market, as a company, the client are prioritizing only the best and most consistent market segment in terms of profitability.
I want to see which market segment is the most consistently profitable. And then, I want to forecast the sales for that most consistently profitable market-segment only. This way I know that the market region your company is investing in will be beneficial for the company as the forecasts will be reliable.

### How to find the most profitable segments?
In order to do so we need to use a metric called Coefficient of Variation (CoV). The CoV is nothing but a ratio of the standard deviation to the mean of the data being calculated for.

The question which arises is instead of choosing the standard deviation which measure the amount of variation present for the 21 market segements we are using CoV. 
The reason is after calculating the mean and standard deviation for the 21 marker segments, these values vary alot and it is difficult to make sense out of them and compare profit using them. 
The CoV normalizes the standard deviation with the mean and produces a comparitive figure on which the profit of each segments can be calculated. The value of CoV which have less variance are taken as the show less variance in the profits. 

### Data Understanding and Preparation
= Find the 21 unique Market Segments by combining the respective 7 geographical markets for each of 3 segments such as Home office, Consumer and Corporate. The dataset after the above step should have Order-Date, Sales, Profit against each market segment such as APAC-Consumer, APAC-Home Office and so on.
- We need to combine the data in month-year format. This will lead us to having data for 48 months. We need to aggregate the data into monthly aggregate transaction date.
- We divide the data into training and testing (42 - 6)
- Calculating the CoV for each market segment.
- Finding the most profitable out of the 21.
- Producing a dataset of the following columns order, sales, profit, market segement. 

Once the most profitable market segement is found we need to perform time series analysis on it. 
 
Based on the observations from the decomposition plots (trend, seasonality and residual components) we need to decide which timeseries models we need to employ.
These algorithms can be divided into two categories smoothing techniques and ARIMA set. We will use MAPE as an evaluation metric.

Steps:
- Train test split for that market segment (dropping the others)
- Decompose the timeseries to get an idea of the trend, seasonality and residual parts.
- The models used are 
    1).  Simple exponential smoothing
    2).  Holt’s exponential smoothing
    3).  Holt-Winters’ exponential smoothing - Additive
    4).  Holt-Winters’ exponential smoothing - Multiplicative
    5)   AR model
    6)   MA model
    7)   ARMA model
    8)   ARIMA model 
    9)   SARIMA model

For the ARIMA set we need to perform the boxcox transformation and differencing to make the timeseries stationary. Lambda is chosen as 0.
The MAPE value for each model is added to a table and comapared with the rest. To choose the best forecasting model from both the smoothing and ARIMA sets.
