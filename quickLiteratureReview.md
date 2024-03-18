# Related paper read： Multivariate Time Series Diagnose and Cause-Inference



### 1 Detecting_Leaders_from_Correlated_Time_Series.pdf

leading metrics + lagged correlation 

The comprehensive relationships among multiple data streams are very helpful in many applications to monitor and control the overall movement of the entity where the data streams are generated. 

analysts only need to monitor and analyze leaders in order to evaluate the overall entity movement triggered by events; leaders have the predictive power within the computed lag. Therefore, analyzing leaders can detect the trend of an event at an early stage.

### 2 AutoMap

[WWW 2020 | 多维时间序列间的异常关联与因果推断_多因素时间跨度下事件关联分析-CSDN博客](https://blog.csdn.net/weixin_53741275/article/details/111973738)

To identify the root cause of anomaly. 

动机： 

1. Even if we know the calling dependency of services, we lack a more dynamic diagnosis mechanism due to the existence of indirect fault propagation.
2. Besides, algorithm based on single metric usually fail to identify the root cause of anomaly, as single type of metric is not enough to characterize the anomalies occur in diverse services.

so we need:

(插入实际情况结合具体案例)

 Dynamic application structure: Due to the various nature of services, static troubleshooting approaches such as thresholding schemes may fail to obtain reliable model applies for frequently changing situations.

Indirect anomaly propagation: time laggaed 

Multiple types of metric： Algorithm based on single metric may fail to identify the root cause, as single type of metric is not enough to characterize the anomalies occur in diverse services. In addition, the asynchronous calling procedures makes metrics often unable to directly reflect the propagation dependency. we still need an automated mechanism that selects them appropriately according to the characteristics of involved services.

### 3 Correlating events with ts for incident diagnosis

three important aspects of event-timeseries correlation in the context of incident diagnosis: existence of correlation, temporal order, and monotonic effect.

Most telemetry data can be grouped into two categories: continuous time series data and temporal event data. 

* A time series is a sequence of real-valued data points, measured typically at successive time points equally spaced with a uniform time interval.
* An event sequence in an online service is used to record the occurrences of a specific software message indicating that something has happened in the system

**correlation analysis** between telemetry data and system states plays a very important role [7] because correlation relationships often provide hints for causality analysis. Although the correlated metrics may not exactly be the root causes of incidents, they could be intermediate useful information that pinpoints the root causes.

**traditional correlation analysis,** such as Pearson correlation and Spearman correlation [8], often cannot provide satisfying results. 

Furthermore, in a large-scale system, an occurrence of an event may be related to a change of a time series during a time period rather than a point-to-point corresponding relationship in the traditional correlation analysis techniques.
