<!--
 * @Author: error: error: git config user.name & please set dead value or install git && error: git config user.email & please set dead value or install git & please set dead value or install git
 * @Date: 2023-11-02 12:57:30
 * @LastEditors: error: error: git config user.name & please set dead value or install git && error: git config user.email & please set dead value or install git & please set dead value or install git
 * @LastEditTime: 2023-11-07 13:29:30
 * @FilePath: \WorkNote\metricsCorrelation.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

# Metrics Correlation Paper Reading

11/02/2023 Kewei Zhang

## 1 Algo 1: Coflux

Question list:

1. Flux-Correlation: Determing the existence of flux-correlation between two metrics
2. Temporal order of flux-correlation: For flux-correlated metrics, undertsanding the temporal order of their fluctuations
3. Direction of flux-correlation: Determining the direction of flux-correlation

First we want to find the best timeseries models as our flux-feature detectors. The question is each model can only fits well with some specific types of characteris of time series. Therefore we decide to apply several well-accepted models together with corresponding parametrs as flux-feature detectors. The two main intuitions are:
A. At least we can find one or more models to fit our given metrics.
B. If two metrics are correlated, then at least one flux-feature of each of them are correlated.

### 1.1 Feature Engineering

Selecting 7 widely-used models to generate flux-features.
Assume time series S = {$s_1,s_2,...s_n$}, for each detector we can get one prediction series P = {$p_1,...p_n$}. Therefore we can have one fluctuation series E = {$e_1,...e_n$}, where $e_i = s_i - p_i$, $1 \leq i \leq n$.

![Alt text](image.png)

#### 1.1.1 Wavelet

Wavelet transformation: a measure of similarity the basis functions(wavelets) and the original function. The coefficients calculated how close the function is to the wavelet at the particular scale. Works better for dynamic(unstationary) signals

discrete wavelet transformation:

decompose the signals into a set of high-frequency and low-frequency signals

[小波变换之离散小波变换-CSDN博客](https://blog.csdn.net/qq_43819404/article/details/134488265#:~:text=%E7%A6%BB%E6%95%A3%E5%B0%8F%E6%B3%A2%E5%8F%98%E6%8D%A2%E7%9A%84%E4%B8%80%E7%BA%A7%E5%88%86%E8%A7%A3%E5%85%AC%E5%BC%8F%E5%A6%82%E4%B8%8B%EF%BC%9A%20A1%28n%29%20%3D%20k%E2%88%91%20f%20%28k%29%E2%88%97h%28k%20%E2%88%92n%29%20D1%28n%29,D1%28n%29%20%E6%98%AF%E9%AB%98%E9%A2%91%20%28%E7%BB%86%E8%8A%82%29%E7%B3%BB%E6%95%B0%E3%80%82%20h%28k%29%20%E5%92%8C%20g%28k%29%20%E5%88%86%E5%88%AB%E6%98%AF%E5%B0%8F%E6%B3%A2%E5%88%86%E6%9E%90%E6%BB%A4%E6%B3%A2%E5%99%A8%E7%9A%84%E4%BD%8E%E9%80%9A%E5%92%8C%E9%AB%98%E9%80%9A%E6%BB%A4%E6%B3%A2%E5%99%A8%E7%B3%BB%E6%95%B0%E3%80%82%20%E7%A6%BB%E6%95%A3%E5%B0%8F%E6%B3%A2%E5%8F%98%E6%8D%A2%E5%85%81%E8%AE%B8%E4%BF%A1%E5%8F%B7%E5%9C%A8%E4%B8%8D%E5%90%8C%E5%B0%BA%E5%BA%A6%E4%B8%8A%E7%9A%84%E5%88%86%E8%A7%A3%E5%92%8C%E9%87%8D%E6%9E%84%EF%BC%8C%E4%BB%A5%E4%BE%BF%E5%88%86%E6%9E%90%E4%B8%8D%E5%90%8C%E9%A2%91%E7%8E%87%E6%88%90%E5%88%86%E3%80%82)

[时间序列信号处理（五）——小波变换python实现_python 小波变换-CSDN博客](https://blog.csdn.net/abc1234abcdefg/article/details/123517320)

N: 采样率 (Hz）, 定义了每秒从连续信号中提取并组成离散信号的采样个数

Fs: , 最高频率， Fs >= 2.5 fmax,通常用2.56 （256 = 2^8）

Fn: Nyquist frenquency, Fn = Fs/2, usually

## 2 Causal Inference

### 2.1 Granger Causality

Granger casuality test: if the G-causes exists. (on stationary test)

#### 2.1.1 Stationary test

ADF test:

```python
if p < 0.05:   
	series is definetely nonstationary;
elif t-statistic < Critical values 10%:
	series is stationary;
else: series is nonstationary
```

KPSS test:

```python
if t-statistic > all critical value:
	series is nonstationary
```

if KPSS shows stable while ADF shows non --> trendy stationary, remove trend

if KPSS shows non while ADF shows stable --> diff stationary, apply diffential

### 2.2 PCMCI

[paper笔记-Detecting causal associations in large nonlinear time series datasets - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/356545365)

[论文阅读：《Inferring causation from time series in Earth system sciences》_pcmci算法-CSDN博客](https://blog.csdn.net/jining11/article/details/108853654)

[因果发现算法概览 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/658985282)

[举例使用因果关系库：TIGRAMITE-CSDN博客](https://blog.csdn.net/qq_36998146/article/details/130838944)

case study : [tigramite/tutorials/case_studies/climate_case_study.ipynb at master · jakobrunge/tigramite (github.com)](https://github.com/jakobrunge/tigramite/blob/master/tutorials/case_studies/climate_case_study.ipynb)

[tigramite/tutorials/dataset_challenges/tigramite_tutorial_missing_masking.ipynb at master · jakobrunge/tigramite (github.com)](https://github.com/jakobrunge/tigramite/blob/master/tutorials/dataset_challenges/tigramite_tutorial_missing_masking.ipynb)

[bsts-causal_impact/Spot_IO_Causal_Impact_Vale_Dam_Accident_20210104.ipynb at main · cmp1/bsts-causal_impact (github.com)](https://github.com/cmp1/bsts-causal_impact/blob/main/Spot_IO_Causal_Impact_Vale_Dam_Accident_20210104.ipynb)


[跟着开源项目学因果推断——CausalImpact 贝叶斯结构时间序列模型（二十一） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/449739638)

[大白话谈因果系列文章（一）：因果推断简介及论文介绍 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/397796913)

### 2.3 Time series

[时间序列因果推断：问题、方法和模型 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/640365578)


### 2.4 doWhy

[因果推断框架 DoWhy 入门 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/321808640)


### 2.5 CausalML

[uber/causalml: Uplift modeling and causal inference with machine learning algorithms (github.com)](https://github.com/uber/causalml)


### 2.6 EconML

[py-why/EconML: ALICE (Automated Learning and Intelligence for Causation and Economics) is a Microsoft Research project aimed at applying Artificial Intelligence concepts to economic decision making. One of its goals is to build a toolkit that combines state-of-the-art machine learning techniques with econometrics in order to bring automation to complex causal inference problems. To date, the ALICE Python SDK (econml) implements orthogonal machine learning algorithms such as the double machine learning work of Chernozhukov et al. This toolkit is designed to measure the causal effect of some treatment variable(s) t on an outcome variable y, controlling for a set of features x. (github.com)](https://github.com/py-why/EconML)

### 2.6 DL

[ICML 2021 | 针对图神经网络的通用因果解释方法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/392206312)

## 3 Detecting leadership

blank here




## 4References

[WWW 2020 | 多维时间序列间的异常关联与因果推断_异常时间点和运维事件的关联性计算-CSDN博客](https://blog.csdn.net/weixin_53741275/article/details/111973738)
