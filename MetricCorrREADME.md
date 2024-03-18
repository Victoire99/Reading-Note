<!--
 * @Author: error: error: git config user.name & please set dead value or install git && error: git config user.email & please set dead value or install git & please set dead value or install git
 * @Date: 2023-11-07 13:29:44
 * @LastEditors: error: error: git config user.name & please set dead value or install git && error: git config user.email & please set dead value or install git & please set dead value or install git
 * @LastEditTime: 2023-11-14 10:42:14
 * @FilePath: \WorkNote\metricCorrCodeExplan.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

# Metirc Correlation Code working flow

在metric correlation 工作中的一些思考发现，相关数据支撑和代码思路解释

### 1 Method


#### 1.1 Holt-Winters

利用三次指数平滑来做时间序列预测

First: $s_i$ 代表第i时刻的平滑估计，由当前实际值$x_i$和上一时刻的平滑估计的加权组成，权重参数为$\alpha$

$$
s_i = \alpha x_i + (1-\alpha)s_{i-1}\\ = \alpha \sum_{j=0}^i(1-\alpha)^j x_{i-j}, \\ \text{where } 0 \leq \alpha \leq 1
$$

Second: 加上趋势 $t_i$, 代表连续两个时刻的差值

$$
s_i = \alpha x_i + (1-\alpha)(s_{i-1}+t_{i-1})\\
t_i = \beta(s_i-s_{i-1}) + (1-\beta)t_{i-1}
$$

Third: 加上季节性因素 $p_i$, 当前季节性值和上一个周期季节性估计值的加权组合，周期为k

$$
s_i = \alpha(x_i-p_{i-k})+(1-\alpha)(s_i-1+t_{i-1})\\
t_i = \beta (s_i - s_{i-1})+(1-\beta)t_{i-1}\\
p_i = \gamma(x_i-s_i)+(1-\gamma)p_{i-k}
$$
