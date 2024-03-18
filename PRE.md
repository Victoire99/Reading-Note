## Intro

Most telemetry data can be grouped into two categories: continuous time series data and temporal event data.

* A time series is a sequence of real-valued data points, measured typically at successive time points equally spaced with a uniform time interval.
* An event sequence in an online service is used to record the occurrences of a specific software message indicating that something has happened in the system

## Raw data visualization

datadog

## Data preprocessing

1. interpolation:
2. clustering: Robust and Rapid Clustering of KPIs for Large-Scale Anomaly Detection

Data Engineering

1. stationary test
2. transfer the series to stationary series

只有同阶单整序列才可以做格兰杰因果检验

做协整检验（**Cointegration**）看是否有长期均衡关系

for long time series, 需进行差分/移动平均 转换为平稳序列，但例子中的数据只有一周，实际应用中最长也只有一个月，没什么意义，所以这里就先不做

## Correlation analysis

到这里就进入我们的计算部分，对于我们现有的数据目前最大的一个问题是由于服务器存储数据的设置我们最长只能有一个月的数据，而这对于任何常规的时间序列计算而言都是不够的，如果我们想要达成我们目标的错误诊断-即寻找根原因，那我们就只能采取一些曲线救国的手段。在这里的解决方法是采取多种不同的数学计算方法，并且我会先计算correlation再计算causal and inference, 把得到的所有的结果结合起来看；

three important aspects of event-timeseries correlation in the context of incident diagnosis:

**existence of correlation/dependency**

Although statistical correlation is not sufficient to demonstrate the presence of a causal relationship, it is still quite useful for incident diagnosis because it can often provide hints to engineers for causal analysis/ correlation relationships often provide hints for causality analysis. Although the correlated metrics may not exactly be the root causes of incidents, they could be intermediate useful information that pinpoints the root causes.

**temporal order of dependency**

which is cause and which is effect

**monotonic effect**

some event occurrence is related to a significant valueincrease (or value-decrease) of a time series. Such a positive (or negative) monotonic effect between two dependent data streams is also a very important property of correlation for causal inference.

**Method:**

1. pearson correlation

   皮尔森相关性系数是一个介于-1和1之间的值，用于度量两个变量之间的线性关系的强度和方向。

   * 如果皮尔森相关性系数接近1，那么这两个变量之间存在强烈的正线性关系。这意味着当一个变量增加时，另一个变量也会增加。
   * 如果皮尔森相关性系数接近-1，那么这两个变量之间存在强烈的负线性关系。这意味着当一个变量增加时，另一个变量会减少。
   * 如果皮尔森相关性系数接近0，那么这两个变量之间的线性关系较弱，或者说几乎没有线性关系。

   皮尔森相关性系数只能度量线性关系，对于非线性关系，它可能会给出误导性的结果。此外，即使皮尔森相关性系数很接近0，这并不意味着两个变量之间没有任何关系，它们可能存在非线性关系或者复杂的依赖关系
2. 斯皮尔曼等级相关性

   函数返回两个值：相关性和p值。相关性是一个介于-1和1之间的数，表示 `x`和 `y`之间的相关程度。p值是一个介于0和1之间的数，表示相关性的统计显著性。
3. Kendall

   [Pearson, Spearman, Kendall 三大相关系数简单介绍 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/60059869)

**traditional correlation analysis,** such as Pearson correlation and Spearman correlation [8], often cannot provide satisfying results.

Furthermore, in a large-scale system, an occurrence of an event may be related to a change of a time series during a time period rather than a point-to-point corresponding relationship in the traditional correlation analysis techniques.

## No statistics method

we can settle with simple static thresholds but :

* intuitive to operators although unsatisfying in detection performance
* after time-consuming manual tuning by algorithm designers, end up with a detector specifically tailored for the given service, which might not be directly applicable to other services.
* it is difficult to precisely define anomalies in reality: impossible for the operators to quantitatively define anomalies, let alone to translate the vague definition into specific parameters and thresholds of a detector [21] (e.g., how many times of the standard deviation [1]) . On the contrary, according to our experience of building detection systems with operators, they prefer to describe the anomalies qualitatively, with anecdotal anomaly cases as examples.
* Even if we know the calling dependency of services, we lack a more dynamic diagnosis mechanism due to the existence of indirect fault propagation.
* Besides, algorithm based on single metric usually fail to identify the root cause of anomaly, as single type of metric is not enough to characterize the anomalies occur in diverse services.

so we need:

(插入实际情况结合具体案例)

 Dynamic application structure: Due to the various nature of services, static troubleshooting approaches such as thresholding schemes may fail to obtain reliable model applies for frequently changing situations.

Indirect anomaly propagation: time laggaed

Multiple types of metric： Algorithm based on single metric may fail to identify the root cause, as single type of metric is not enough to characterize the anomalies occur in diverse services. In addition, the asynchronous calling procedures makes metrics often unable to directly reflect the propagation dependency. we still need an automated mechanism that selects them appropriately according to the characteristics of involved services.

## Causal Inference

Granger Inference

请注意，格兰杰因果关系检验的原假设是不存在因果关系。如果p值小于显著性水平（例如0.05），那么我们就拒绝原假设，认为存在因果关系。

transfer entropy

why ML:

we advocate for using supervised machine learning techniques, well known for being able to capture complex concepts based on the features and the labels from the data (e.g., KPI data)

1. PCMCI
2. LSTM
