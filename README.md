# fxgen
## Comprehensive Framework for Modelling Market Behavior
This document proposes a framework to model market conditions 

## Leading or Lagging Indicators

## Noise
While our view of previous market conditions is always certain, i.e. with 100% probability, market future carries uncertainty. Different statistical methods could be used to measure market uncertainty in the future.   
Noise could be viewed upon either as a primary or secondary variable in every analysis. 
As a **primary** variable, we evaluate market noise irrespective of any context. Therefore, we would have a noise function $N(t)$ which measures market noise at time $t$ independent of other market variables.
However, as a **secondary** variable, we take into account *market context* in our evaluation of noise. So the noise function becomes $N(t, C(M_t))$ where $C(x)$ is a context function and $M_t$ is a bundle of market variables at time $t$.
## Predictability 
Predictability evaluates how robust a lagging indicator could perform as a leading indicator. In our market model, when **noise** is 0, any lagging indicator could perfectly predict future state and therefore, predictability is 1.     
## Range or Trend
Principles:

 1. Range or trend should be modeled as a continuous spectrum rather than two states.
 2. Every indicator attempting to model range or trend is a lagging indicator

> Written with [StackEdit](https://stackedit.io/).
