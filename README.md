# Xnomer Moving Average
Often in financial market technical analysis, one faces the problem of deciding which period of (simple or exponential) moving averages to use. While the moving average periods of 9, 20, 50, 100, and 200 are commonly used, some argue that certain other periods serve better for technical analysis in some cases. The problem actually lies on the fact that prices volatility changes over time. MACD indicators with shorter periods typically perform better in highly volatile charts such as that of Bitcoin. A mismatch between price fluctuation frequency and MACD periods could yield false signals. Hence, it is desirable to have an indicator that adapts to the changes in volatility. **Xnomer Moving Average** (XMA) is one possible form of such indicators.

In exponential moving average (EMA), the indicator value changes at a constant proportional rate, *k* := 2 / (*period* + 1), to the current price, *x*<sub>t</sub>.

<p align="center">
  <em>EMA</em><sub>t</sub> = <em>k</em> <em>x</em><sub>t</sub> + (1 - <em>k</em>) <em>EMA</em><sub>t-1</sub>.
</p>

The coefficient *k* should ideally changes with changing volatility. One way to achieve this is to make *k* dependent on the changes in price: *k* := *k*(Δ*x*). A noteworthy characteristic of *k*(Δ*x*) is that Δ*x* can be infinite, whilst *k* is bounded between 0 and 1. Another is that *k* should increase with Δ*x*. Two standard functions that satisfy these properties are tanh(|*x*|) and arctan(|*x*|). tanh(*x*) and arctan(*x*) are bounded between -1 and 1 as shown in the figure below. Hence, tanh(|*x*|) and arctan(|*x*|) are bounded between 0 and 1.

![tanh and arctan](/tanh-and-arctan.jpg)

XMA is defined as having the form of EMA,

<p align="center">
  <em>XMA</em><sub>t</sub> := <em>k</em> <em>x</em><sub>t</sub> + (1 - <em>k</em>) <em>XMA</em><sub>t-1</sub>,
</p>

but with the coefficient *k* being a function of the changes in price, Δ*x*, relative to the standard deviation as follows:

<p align="center">
  <em>k</em><sub>t</sub> := (2 / π) arctan((π / 2) <em>c</em> |Δ<em>x</em>| / <em>STDEV</em><sub>t</sub>),
</p>

where *c* is called the elasticity constant and *STDEV* is a moving standard deviation in price. *STDEV*<sub>t</sub> is calculated over a moving window of fixed length, *L*.

In a sense, XMA is an EMA where the period changes with the volatility. A distinct characteristic of XMA, compared to EMA, is that it is more responsive to increasing volatility and less responsive to decreasing volatility relative to the recent past, as illustrated in the EURUSD chart below. In this example, the XMA is calculated with *c* = 0.1 and *L* = 50.

![EURUSD example](/EURUSD-20211211.png)

Whether XMA is a better indicator than EMA is a subject of lengthy research, which is left as an exercise for the reader.

A pine script to calculate XMA on TradingView is provided in this repository.

## Licensing
This work is licensed under the [Apache Public License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
