# Framework
This document proposes a framework to model market conditions 
## Market 
We use the term market a lot in this document. In fact, the main goal of this document is to provide a pseudo-mathematical foundation for market modelling. 
We use $M_t$ notation to describe market state at time $t$. This is also referred to as bundle of market variables at time $t$. **Market variables** in this context are the lowest-order data which could be used to describe market conditions.

The lowest order data which an analyzer has access to is **tick data**. Every tick defines the value (or price) of market at time $t$. We denote this by $Tick_t$. Therefore, $M_t$ could be defined as a series of tick data:

$M_t :=\\{...,Tick_{t-2}, Tick_{t-1}, Tick_t\\}$

One way to model market is by using **context functions**. A context function, in our definition, takes a bundle of market variables and provides a higher-order description of market. Context functions could have recursive nature. 

In this definition, **indicators** are a subset of context functions.

Therefore, OHLC model is a 4-dimensional, higher-order context function defined as below:

$C_{ohlc}(M_t) = O_t, H_t, L_t, C_t$

$O_t = Tick_{t-P}$

$H_t = max(Tick_{t-P},...,Tick_t)$

$L_t = min(Tick_{t-P},...,Tick_t)$

$C_t = Tick_{t}$
 
## Indicator
An indicator encapsulates market context into a single or multi-dimensional value. 
Indicators are always **lagging** in our definition, meaning they observe previous market conditions. 
Indicators could provide **leading** functionality and this could be measured using the notion of **predictability**.
The formal definition of an indicator is:

$I(t) = f(C(M_t))$

where $C(x)$ is a context function and $M_t$ is a bundle of market variables at time $t$.
## Noise
While our view of previous market conditions is always certain, i.e. with 100% probability, market future carries uncertainty. Different statistical methods could be used to measure market uncertainty in the future.   
Noise could be viewed upon either as a primary or secondary variable in our analysis. 
As a **primary** variable, we evaluate market noise irrespective of any context. Therefore, we would have a noise function $N(t)$ which measures market noise at time $t$ independent of other market variables.
However, as a **secondary** variable, we take into account *market context* in our evaluation of noise. So the noise function becomes $N(t, C(M_t))$ where $C(x)$ is a context function and $M_t$ is a bundle of market variables at time $t$.
## Predictability 
Predictability evaluates how robust a lagging indicator could perform as a leading indicator predicting a future market state. In our market model, when **noise** is 0, any lagging indicator could perfectly predict future state and therefore, predictability is 1. 

To define predictability in this setup, we have an indicator $I$, a context function $C$ and a look-forward period $T$ where we expect our indicator to predict. 

Also, we define function $P_{I,C}$ as prediction function of indictaor $I$ under context function $C$, formally defined as $P_{I,C}(t, T) -> predictedC_{t+T}$. This function predicts market at T periods in the future using indicator value a time $t$. 

Predictability would be defined as $Pred_{I,C}(t, t+T)$. Predictability measures deviation of predicted price using $P_I$ from actual price at T period of times in the future. Predictability is a **loss function** in nature and any viable loss function used in machine learning could be utilized to measure predictability.

$Pred_{I,C}(t, t+T) = Loss[P_{I,C}(t, T), C(t+T)]$

One naive definition could be L1 norm:

$Pred_{I,C}(t, t+T) = 1 - |P_{I,C}(t, T) - C(t+T)| / C(t+T)$

In a perfect scenario, where $I(t)$ precisely predicts market at $t+T$, the above equation would equal to 1. any deviation of $I(t)$ from $C(t+T)$ would result in predictability to become less than one.

As could be easily observed, our definition of predictability is itertwined with our notion of market, i.e. the context function, and how we define loss function. For example, if we define our context function to be the closing market price (**C** in OHLC model), L1 norm could be a perfectly good candidate for loss function. However, considering the case where our context function is an exponentially smoothed average of market prices, then perhaps we should revisit our definition of loss function and use a higher order norm.
    
## Range or Trend
Markets are either ranging or trending. To understand the ranging or trending status of market is crucial for any trading agent to be able to adjust its trading and risk management strategy. Obviously, in a trending market, following the old saying of *"Trend is Your Friend"* is the optimal strategy and one should not take positions against the trend. On the other hand, in a range market, *mean-reversion strategies* often provide the best results. 

We observe following principles in our definition and modelling of range/trend:

 1. Range or trend should be modeled as a *continuous spectrum* rather than two discrete state.
 2. Range or trend is modeled against a time granularity.

