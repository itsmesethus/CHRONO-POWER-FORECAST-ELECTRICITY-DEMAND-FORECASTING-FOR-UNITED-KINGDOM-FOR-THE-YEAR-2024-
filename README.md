
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

- [Introduction](#Introduction)
- [Data Preprocessing](#Data-Preprocessing)
- [Data Visualization](#Data-Visualization)

      # Part 1 : STATISTICAL MODELS & FB-Prophet

- [Seasonal Decomposition](#Seasonal-Decomposition)
- [Statistical Test for Stationarity](#Statistical-Test-for-Stationarity)
- [Statistical Models & FB-Prophet](#Statistical-Models-&-FN-Prophet)

      # Part 2 : DEEP LEARNING MODELS Based on Sequences

- [Data Preprocessing for Deep learning Architectures](Data-Preprocessing-for-Deep-Learning-Architectures)
- [Deep Learning Architectures Based on Sequences](#Deep-Learning-Architectures-Based-on-Sequences)

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

## **Part 1:**

## Seasonal Decomposition:

   Using the Statsmodels library, visualized the both Multiplicate and Additive models for Seasonal Decomposition for EWD, TSD and ND.
               
      Terminologies:

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

## Train-Test-Split For Time Series Data:

   Shuffling time series data disrupts its natural order, leading to inaccurate modeling and forecasting. It can cause data leakage, where future information influences past predictions, and it undermines realistic model evaluation. Instead, split the data chronologically to train on past data and evaluate on future data, ensuring accurate performance assessment.

   Ex: To predict the Nth value in a time series, the model needs the correct sequence of values from 1 to (N-1) to learn the patterns and trends effectively. Shuffling the data could mix up this sequence, leading to inaccurate predictions because the model 

   So, without shuffling the data I took last 180 data pts as my testing set for ND, TSD and EWD and rest as training data.

## Statistical Models & FB-Prophet:

  I have used the following below models in my part 1 for forecasting,

   **@ Simple Exponential Smoothing Model**

      * The simplest form of exponential smoothing. This model entirely depends upon the single parameter called as smoothing factor or alpha which adds the extra weight to recent past observations and decling alpha values for rest of observations in the data series.

      * SES is suitable when TS does not possesses trend or seasonality but it will have constant level. One of the best thing about SES is it wil provide smooth and stable forecasts but cannot tackle the problem of quick changes in data.

      * SES= (alpha * nth-observation(t)) + (1-alpha) * (Forecast (t))

      * Smoothing factor, alpha values always lies between 0 and 1.   

   **@ Double Exponential Smoothing Model**

      * Also known as Holt's linear exponential Smoothing method which additionally incorporates the extra trend parameter(beta) to the simple exponential smoothing-smoothing parameter(alpha) to the model. These models works under the principle of weighted avaerage methods which the recent past observations gets the extra weights than the rest of observations in the series.

      * Holt's linear model has equations for calculating level and trend for below,

      a)Level

      Forecast(t+1) = (alpha * Observation(t)) + (1-alpha) * (Forecast(t) + Trend(t) )

      b) Trend

       Trend(t+1) = beta * (Forecast(t+1) - Forecast(t)) + (1-beta) * (Trend(t))

      One of the disadvantage of the model is, seasonality may not be incroporated here. And also it assumes that trend is constant over time which is not in the reality.


   **@ Triple Exponential Smoothing Model**


      * Also known as Holt-Winters Exponential Smoothing method where it is the upgraded versions of single and double exponential methods. and additionaly incorporates the Seasonality(gamma)as extra factor consider for forecasting the future values.

      * Seasonality factor(gamma) tackles the periodic fluctuations in the TS data.

      * Equations are

         a) Level = (alpha) * ( observation(t) - Seasonal of (t-lenth of cycle)) + (1-alpha) * (Smoothed Observation of (t-1) + Trend factor of (t-1)).

         b) Trend = (beta) * (Seasonal of (t) - Seasonal of (t-1)) + (1-beta) * (trend of (t-1))

         c) Seasonal = (gamma) * (observation(t) - Seasonal(t)) + (1- gamma) * (Seasonal of (t- length of cycle)).   
      

   # **Correlation Plots:**

   **ACF(Auto-Correlation Function)**

      * ACF plot used to identify the order of AutoRegression model(AR).
      * The order of an AR model is the no of lags that are included in the model.
      * The ACF plot will show spikes at the lags that are included in the model.
      * Any lags that are out of the filled margin boundaries are said to be significant lags.
      * ACF accounts for both direct and indirect effects of the lags.

   **PACF(Partial-Auto-Correlation Function)**

      * PACF plot used for identify the significantly contribution lags for modelling Moving Average(MA) model.
      * PACF only accounts the direct effects of the lags, which means it removes the effects of the previous lags.
      * Similarly, which ever lags are notched out of the margin boundaries are considered as significant lags for MA modelling.

   **@ AutoRegressive Model**

      * An AR(p) model relies only on the past period values to predict current ones.
      * It's a linear model, where current period values are a sum of past outcomes multiplies by a numeric factor.
      * Here the order p represents the no of significant correlated lags should be included in the model for forecasting the future.  
      * AR(p=1) equation is given below,
      
![screenshot.png](https://github.com/itsmesethus/CHRONO-POWER-FORECAST-ELECTRICITY-DEMAND-FORECASTING-FOR-UNITED-KINGDOM-FOR-THE-YEAR-2024-/blob/main/pics/ar1.png)


**@ Moving Average Model**

      * MA model relates the current value of the series to past error terms. 
      * It captures the shocks or unexpected events in the past that are still affecting the series.
![screenshot.png]( https://github.com/itsmesethus/CHRONO-POWER-FORECAST-ELECTRICITY-DEMAND-FORECASTING-FOR-UNITED-KINGDOM-FOR-THE-YEAR-2024-/blob/main/pics/ma1.png)

**@ AutoRegressive Moving Average Model (p,q)** 

      * It is a combination of two models such as AR and MA.
      * Here the impact of previous lags along with the residuals  is considered for forecasting the future values of the TS.
      * It is used to describe weakly stationary stochastic time series.

![screenshot](https://github.com/itsmesethus/CHRONO-POWER-FORECAST-ELECTRICITY-DEMAND-FORECASTING-FOR-UNITED-KINGDOM-FOR-THE-YEAR-2024-/blob/main/pics/arma.png)

      * yt and yt-1 -  values in current preriod and 1 period ago.
      * ϵt and ϵt−1 - error terms for the same two periods( where the error term from last period is used to help correct our forecasting)
      * C - constant
      * ϕ1 - express on what part of the value last period is relevant in explaining the current one.
      * θ1- represents the same for the past error term
      
**@ Seasonal Auto Regressive Moving Average (p,d,q) (P,D,Q,s)**

      1) A similar model to ARMA but the only difference is incorporating the seasonal factor within the model with some extra prameters.
      2) This model will be really handy when we are dealing with seasonal datasets.
      3) Non seasonal parameters are (p,d,q)
      4) Seasonal Parameters are (P,D,Q,s)
      5) where, 
         * P- Seaonal AR order
         * D- Seasonal Integration Order
         * Q- Seasonal MA order
         * s- Length of cycle (ex:24 hrs, 12 months and etc...)
      6)the best way to estimate seasonal_order(sp,sd,sq,s) parameters.
      parameters:

         * 1 for yearly
         * 4 for quarterly
         * 12 for monthly
         * 52 for weekly
         * 365 for daily
     7)s=1, When dealing with non seasonal time series dataset

**@ FB-Prophet model**


      1) Prophet was introduced by Taylor and Letham in 2018 and this model structure is given as,

            Time Series = Signal + Noise

         where, Signal part-> Forecasts extrapolate signal portion of model and Noise part -> Confidence interval accounting for uncertainity.

      2) Signal part is composed of Trend/Growth, Seasonal and Holiday.

          * Trend/Growth - uses trend lines(time) as regressors in the model and if there is no linear trend observations will be broken into different pieces of the data using knots.

         * Seasonal - Here it uses the Fourier variables to account for seasonal patterns.Fourier showed that series of sine and cosine terms of right frequencies approximate periodic series. So, it expanded flexibility on seasonal terms.

          * Holiday - Which is a point intervention variable or binary indicator of certain day.

      3) Prophet does not use any lags of the target variable. In a nutshell, a curve fitting approach to forecasting. Forecasting just extends the curves into the future.


## **PART 2:**

## Data Preprocessing for Deep Learning Architectures:

      1) Extract the values in the dataframe in separate variables and reshape into a proper dimensions.
      2) Using the scaler transformation for conversition.
      3) Created a function which should intake the data and time steps for forecasting the time series sequences.
      4) The main features are National Demand, Transition System Demand and England and wales demand of Electricity and so our features are 3.And using that create a single model with 3 output features for forecasting the year 2024.

## Deep Learning Architectures based on Sequences

**@ Recurrent Neural Network Model**

      * Recurrent neural network is a type of neural network used to deal specifically with sequential data. 
      * It actually works with the current input from the data and the previous input of the data.
      * Important feature of the RNN is its Hidden State(Memory State) which helps it to memorize the input data to the network.And Simple RNN model posses single gate.  
      * Hidden State Update Gate:
         Purpose: Computes the new hidden state based on the current input and the previous hidden state.
         Activation: Typically uses a hyperbolic tangent (tanh) or another activation function.

**@ Bidirectional Recurrent Neural Network Model**

      * A Bidirectional Recurrent Neural Network (RNN) is an extension of the traditional RNN architecture that processes input sequences in both forward and backward directions. 
      * This allows the network to capture dependencies from past and future contexts, enhancing its ability to understand sequential data.
      * The outputs from both directions are typically concatenated or combined in some way to generate the final output sequence.

**@ Long Short Term Memory Model** 

      * Long Short-Term Memory (LSTM) is one of the (RNN) architectures designed to address the vanishing gradient problem in traditional RNNs. 
      * This architecture is  particularly useful in tasks where sequences and dependencies play a crucial role, such as natural language processing, speech recognition, and time series analysis. And its gates are,

      * Forget Gate:

         Purpose: Determines what information from the cell state should be discarded or kept.
         Activation: Sigmoid function.

      * Input Gate:

         Purpose: Determines what new information to store in the cell state.
         Activation: Sigmoid function.

      * Cell State Update:

         Purpose: Updates the cell state with new information.
         Activation: Tanh function.

      * Output Gate:

         Purpose: Determines the next hidden state and also the output of the cell.
         Activation: Sigmoid function

**@ Bidirectional Long Short Term Memory Model**

      * Bidirectional Long Short-Term Memory (LSTM) is an advanced variation of the LSTM architecture that processes input sequences in both the forward and backward directions simultaneously.
      * This enables the network to capture information from both past and future contexts, enhancing its ability to understand and model sequential data.
      * Bidirectional LSTM, two sets of LSTM units operate in parallel, one processing the input sequence in the forward direction and the other in the backward direction. 
      * Bidirectional LSTMs maintain separate hidden states for forward and backward processing. These hidden states encapsulate relevant information learned from the input sequence in each direction 

**@ Gated Recurrent Unit Model**
      
       * GRU has a simpler architecture compared to Long Short-Term Memory (LSTM). 
       * It consists of two gates, namely the reset gate and the update gate, which makes it computationally less intensive and easier to train.
       * GRU is often considered effective for capturing short-term dependencies in sequential data. 
       * It may perform well in tasks where retaining recent information is more critical than maintaining long-term dependencies.  

       * Update Gate:

         Purpose: Determines the extent to which the previous memory should be updated with the new information.
         Activation: Sigmoid function.

      * Reset Gate:

         Purpose: Decides how much of the previous memory to forget.
         Activation: Sigmoid function.

      * Hidden State Update:

         Purpose: Computes the new hidden state based on the current input, the previous hidden state (after considering the reset gate), and the updated memory.
         Activation: Typically uses a hyperbolic tangent (tanh) or another activation function. 

**@ Bidirectional Gated Recurrent Unit Model**

      * Bidirectional GRUs follow a similar concept as Bidirectional LSTMs but with the simpler structure of GRUs. 
      * They process input sequences in both directions, maintaining the reset and update gates for each direction.
      * As usual same gates will be here with the GRU.
      * Bidirectional GRUs often have a faster training speed compared to Bidirectional LSTMs due to the simpler structure of GRUs

**@ Hybrid Models (Convolution + LSTM + DNN ) Model**

      * A Hybrid Model combines Convolutional Neural Network (CNN), Long Short-Term Memory (LSTM), and Deep Neural Network (DNN) architectures to leverage their respective strengths in processing different types of data and capturing temporal dependencies in sequential data.

      1) Convolutional Neural Network (CNN): CNNs are effective in extracting spatial features from input data, making them well-suited for tasks such as image classification and feature extraction.

      2) Long Short-Term Memory (LSTM): LSTMs excel at capturing long-range dependencies and temporal patterns in sequential data, making them ideal for tasks like time-series analysis.

      3) Deep Neural Network (DNN): DNNs provide powerful nonlinear modeling capabilities and are often used for high-level feature abstraction and decision making.

**@ Hybrid Models (Convolution + GRU + DNN) Model**


      * A Hybrid Model that combines Convolutional Neural Network (CNN), Gated Recurrent Unit (GRU), and Deep Neural Network (DNN) architectures to leverage their complementary strengths in processing different types of data and capturing temporal dependencies in sequential data.

      1) Convolutional Neural Network (CNN): CNNs excel at extracting spatial features from input data, making them well-suited for tasks such as image processing and object recognition.

      2) Gated Recurrent Unit (GRU): GRUs are a type of recurrent neural network architecture that is capable of capturing long-range dependencies and temporal patterns in sequential data, similar to LSTMs but with a simpler architecture.

      3) Deep Neural Network (DNN): DNNs provide powerful nonlinear modeling capabilities and are often used for high-level feature abstraction and decision making.



For Forcasting the Electricity demand 2024 using all the above models were visualized using line chart.

## References

1) https://www.linkedin.com/advice/0/how-do-you-evaluate-accuracy-exponential-smoothing#simple-exponential-smoothing
2) https://365datascience.com/tutorials/time-series-analysis-tutorials/autoregressive-model/
3) https://ilyasbinsalih.medium.com/what-are-acf-and-pacf-plots-in-time-series-analysis-cb586b119c5d#:~:text=The%20order%20of%20an%20AR%20model%20is%20the%20number%20of,are%20included%20in%20the%20model.&text=The%20PACF%20plot%20is%20a,effects%20of%20the%20previous%20lags.
4) https://www.kaggle.com/code/nholloway/seasonality-and-sarimax
5) https://medium.com/@ritusantra/introduction-to-sarima-model-cbb885ceabe8
6) https://help.rubiscape.io/rarg/forecasting/modeling/sarima
7) https://www.kaggle.com/code/vaibhavsxn/time-series-multivariate-lstm
8) https://www.analyticsvidhya.com/blog/2020/10/multivariate-multi-step-time-series-forecasting-using-stacked-lstm-sequence-to-sequence-autoencoder-in-tensorflow-2-0-keras/
9) https://machinelearningmastery.com/how-to-use-the-timeseriesgenerator-for-time-series-forecasting-in-keras/
10) https://www.geeksforgeeks.org/gated-recurrent-unit-networks/
11) https://deepai.org/machine-learning-glossary-and-terms/gated-neural-network
12) https://www.geeksforgeeks.org/time-series-forecasting-using-recurrent-neural-networks-rnn-in-tensorflow/
13) https://www.kaggle.com/code/fatmakursun/time-series-forecasting-unknown-future
