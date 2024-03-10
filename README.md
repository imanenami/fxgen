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
Predictability evaluates how robust a lagging indicator could perform as a leading indicator. In our market model, when **noise** is 0, any lagging indicator could perfectly predict future state and therefore, predictability is 1. 
    
## Range or Trend
Principles:

 1. Range or trend should be modeled as a continuous spectrum rather than two states.
 2. Every indicator attempting to model range or trend is a lagging indicator
