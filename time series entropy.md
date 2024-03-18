# Time Series Information Representation & Extraction

## 时间序列统计特征

$$
X_T = {x_1,....x_T}
$$

均值：

$$
\mu = \frac{1}{T}\sum_{i=1}^{T}x_i
$$

方差：

$$
\sigma^2 = \sum_{i=1}^T\frac{1}{T}(x-\mu)^2
$$

偏度：

$$
\text{skewness}(X)=E[(\frac{X-\mu}{\sigma})^3]=\frac{1}{T}\sum_{i=1}^T\frac{(x_i-\mu)^3}{\sigma^3}
$$

峰度：

$$
\text{kurtosis}(X)=E[(\frac{X-\mu}{\sigma})^4]=\frac{1}{T}\sum_{i=1}^T\frac{(x_i-\mu)^4}{\sigma^4}
$$

## 时间序列熵特征

熵 entropy:

$$
\text{entropy}(X)=-\sum_{i=1}^\infin P(x=x_i)ln(P(x=x_i))
$$

### Binned Entropy:

分桶：把[min($X_T$),max($X_T$)]该区间等分为十个小区间/桶，根据等距分桶的情况计算出此概率分布的熵

$$
\text{binned entropy}(X)=-\sum_{k=0}^{min(maxbin,len(x))} p_kln(p_k)*1_{(p_k>0)}
$$

$p_k$: $X_T$的取值落在第k个桶的概率

$maxbin$: 桶的个数

$len(X_T)=T$: $X_T$的长度

如果 binnedEn 较大，说明取值均匀分布；如果小。说明集中在某一段上

### Approximate Entropy

把一维空间的时间序列提升到高维空间中，通过高维空间的向量之间的距离或者相似度的判断，来推导出一维空间的时间序列是否存在某种趋势或者确定性

## Ref

[时间序列的表示与信息提取 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/39105270)

[时间序列数据中的熵 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/559915397)

[AI算法Python实现：Transfer entropy_pyinform-CSDN博客](https://blog.csdn.net/daishabby2486/article/details/129355883)
