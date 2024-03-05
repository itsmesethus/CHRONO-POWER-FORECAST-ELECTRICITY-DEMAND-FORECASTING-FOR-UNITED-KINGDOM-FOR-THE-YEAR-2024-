# ProjectTitle: CHRONO-POWER-FORECAST-ELECTRICITY-DEMAND-FORECASTING-FOR-UNITED-KINGDOM-FOR-THE-YEAR-2024


Due to large file size i cant able to upload the file here in github. Instead you can access the files from the below link!!

link:   https://drive.google.com/drive/folders/1VS92OKVZpuz1ZzobgADQgcxsnJ08Gbm0?usp=sharing

Dataset link: https://www.kaggle.com/datasets/albertovidalrod/electricity-consumption-uk-20092022

Thank you. 
Note: If you cant access the files feel free to contact me using the below email id.
email: sethus4791@gmail.com
linkdin: https://www.linkedin.com/in/sethus4791.

*************************************************************************************************************************************

## OBJECTIVE:
  To analyze historical electricity demand data and apply time series forecasting methods to predict the electricity demand for NS, TSD, and England and Wales in 2024.

## VARIABLES:

National Grid ESO is the electricity system operator for Great Britain. They have gathered information of the electricity demand in Great Britain from 2009. The is updated twice an hour, which means 48 entries per day. This makes this dataset ideal for time series forecasting.

* SETTLEMENT_PERIOD: half hourly period for the historic outtunr occurred

* ND (National Demand). National Demand is the sum of metered generation, but excludes generation required to meet station load, pump storage pumping and interconnector exports. National Demand is calculated as a sum of generation based on National Grid ESO operational generation metering. Measured in MW.


* TSD (Transmission System Demand). Transmission System Demand is equal to the ND plus the additional generation required to meet station load, pump storage pumping and interconnector exports. Measured in MW.


* ENGLAND_WALES_DEMAND. England and Wales Demand, as ND above but on an England and Wales basis. Measured in MW.

## LIBRARIES USED:

   - Pandas, Matplotlib, Seaborn, Scikit-learn, datetime, Statsmodels, Tensorflow, Numpy, Keras, FB-Prophet.


## TABLE OF CONTENTS:

- [Introduction](#introduction)
- [Data Preprocessing](#data-preprocessing)
- [Data Visualization](#data-visualization)

      # Part 1 : STATISTICAL MODELS & FB-Prophet

- [Seasonal Decomposition](#seasonal-decomposition)
- [Statistical Test for Stationarity](#statistical-test-for-stationarity)
- [Statistical Models & FB-Prophet](#statistical-models-&-fb-prophet)

      # Part 2 : DEEP LEARNING MODELS Based on Sequences

- [Deep Learning Architectures based on Sequences](#deep-learning-architectures-based-on-sequences)

## Introduction:

  Electricity demand forecasting is a crucial task for energy system operators to ensure the stability and reliability of the grid. Accurate forecasts enable efficient resource allocation, grid planning, and decision-making processes. In this project, we aim to forecast the electricity demand in Great Britain using a dataset provided by the National Grid Electricity System Operator (ESO). I took the data from 2018 to 2023 year and forecast for 2024. So, I would like to proceed this project into 2 phase/parts. Where the first phase is entirely dealing with the Statistical procedures and models and the other phase is where entirely dealing with Sequences based Deep Learning Architectures for Forecasting the year 2024. 

## Data Preprocessing:

   In this part, I have inquired about the data quality such as missing values and any inconsistencies for further consideration for model building part. And also converted the SETTLEMENT_PERIOD  to single day by averaging out the  ND, TSD and EWD.

## Data Visualization:
   
   For Data visualization part, I did

   * Barplots
   * Boxplots for Electricity over months
   * Histograms for the VARIABLES for analyzing their spread
   * Line plot for VARIABLES

## Seasonal Decomposition:

   Using the Statsmodels library, visualized the both Multiplicate and Additive models for Seasonal Decomposition for EWD, TSD and ND.

   @ Trend - long term pattern with either increasing or decreasing manner

   @ Seasonal - Periodical behaviour pattern that often occurs every year cycle of the data.

   @ Residual - random movement patterns which cannot be predicted or modelled easily.

## Statistical Test for Stationarity:

   Inorder, to proceed the Statistical models, I need to ensure that all the VARIABLES conidered must satisfy the Stationarity. Stationarity - A Time series data said to be stationary if its mean and variance does not vary across time. There wont be any trend or seasonality observed in a stationary data. For Statistical Time series modelling, stationarity plays vital role in that area.

Assumptions:

      1) constant mean
      2) constant variance
      3) Constant Autocorrelation

Unit Root:

   Also known as difference stationary process which is a stochastic trend in time series. If a TS has a unit root, it shows a systematic pattern that is unpredicatable. In TS , a unit root signifies that the series is non- stationary in nature. Unit root tests are designed for determining whether differencing is required in the data. Some Unit root test are:

   * Augumented Dickey Fuller Test
   * kiwatkowksi-Philips Schmidt Shin Test

@ AUGUMENTED DICKEY FULLER TEST:

   It is used to check the presence of a unit root in a TS data. Idea behind this medthod is testing whether the coefficient of lagged level of the TS is equal to the AutoRegression(p=1).

 This test can include a constant term, a linear trend term, or both and it entirely depending upon the characteristics of the TS data.

      Hypotheseis St,

      * H0_adf='Data is not Stationary in nature, ie: unit root = 1'
      * H1_adf='Data is Stationary in nature, ie: unitroot < 1'


      Decision: If p value <= alpha value, Reject H0
           If p value > alpha value , Accept H0

@ KIWATKOWKSI PHILIPS SCHMID SHIN TEST:

   KPSS test to check for stationarity in the ‘presence of a deterministic trend’. The word ‘deterministic’ implies the slope of the trend in the series does not change permanently.

   Hypothesis St,

      * H0_kp='Data is Stationary in nature or linear in trend'
      * H1_kp='Data is not Stationary in nature or linear in trend'


      Decision: If p value <= alpha value, Reject H0
           If p value > alpha value , Accept H0

If all these done, assumptions are satisfied, further I can go for the Statistical Model Building Phase or else I cant proceed further.

(Note: For Ensuring Stationarity, i  did the seasonal differencing to remove the non-stationarity. There also other methods exists, such are logarithm, and others... )



Model used for Forecasting,

PART 1:
"" STATISTICAL MODELS AND OTHER ""

@ Simple Exponential Smoothing Model
@ Double Exponential Smoothing Model
@ Triple Exponential Smoothing Model
@ AutoRegressive Model
@ Moving Average Model
@ AutoRegressive Moving Average Model 
@ Seasonal AutoRegressive Moving average model
@ FB-Prophet model


PART 2:
 "" DEEP LEARNING MODELS USED FOR FORECASTING ""

@ Recurrent Neural Network Model
@ Bidirectional Recurrent Neural Network Model
@ Long Short Term Memory Model
@ Bidirectional Long Short Term Memory Model
@ Gated Recurrent Unit Model
@ Bidirectional Gated Recurrent Unit Model
@ ybrid Models (Convolution + LSTM + DNN ) Model
@ Hybrid Models (Convolution + GRU + DNN) Model
