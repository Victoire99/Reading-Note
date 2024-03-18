# Transfer Entropy 转移熵

Shannon Entropy: Information Entropy 信息熵

变量与变量之间信息的传递，计算该信息传递能减少多少被观测系统的不确定性

X, Y: random variable

$$
H(X) = -\sum_xP(x)log_2[P(x)]
$$

事情发生的概率越大，熵越小 --> 熵：事情的不确定性

* 联合熵：

$$
H(X,Y) = -\sum_x\sum_yP(x,y)log_2[P(x,y)]
$$

* Conditional Entropy 条件熵：
  已知Y发生，X的不确定性
* 互信息：是指知道X，对Y的不确定性的减少程度（或知道Y后X的不确定性的减少程度）

$$
H(X;Y) =H(X)-H(X|Y)\\=H(X)+H(Y)-H(X,Y)\\=\sum_xp(x)log\frac{1}{p(x)}+\sum_yp(y)log\frac{1}{p(y)}-\sum_{x,y}p(x,y)log\frac{1}{p(x,y)}\\=\sum_{x,y}p(x,y)log\frac{p(x,y)}{p(x)p(y)}
$$

    边缘概率：$p(x)=\sum_yp(x,y)$

    则我们有：$\sum_xp(x)log\frac{1}{p(x)}=\sum_{x,y}p(x,y)log\frac{1}{p(x)}$

* Relative Entropy/ Kullback-Leibler divergence 相对熵\/KL
  衡量两个概率分布之间的差异

  $$
  D_{KL}(p||q) = \sum_x p(x) log\frac{p(x)}{q(x)}=E_{p(x)}log\frac{p(x)}{q(x)}
  $$
* Transfer Entropy：

  X对Y的传递熵>Y对X的传递熵时，X为因Y为果，建立因果关系
  ⚪面积为信息熵，计算可得图中传递熵$T(X_t>Y_{t,\tau})$的大小

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191211150219454.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FscGhvc2V2ZW4=,size_16,color_FFFFFF,t_70)

  $$
  T(X>Y,\tau)=H(X_{t-\tau},Y_{t-\omega})+H(Y_t,Y_{t-\omega})-H(Y_{t-\omega})-H(X_{t-\tau},Y_t,Y_{t=\omega})\\
  $$

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191211153032412.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FscGhvc2V2ZW4=,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191211153046277.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FscGhvc2V2ZW4=,size_16,color_FFFFFF,t_70)



化简：![在这里插入图片描述](https://img-blog.csdnimg.cn/20191211153627475.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FscGhvc2V2ZW4=,size_16,color_FFFFFF,t_70)










*References*

[香农熵_熵图像与卡尔曼背景模型的使用-CSDN博客](https://theonegis.blog.csdn.net/article/details/79890407?ydreferer=aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTM4MjIwL2FydGljbGUvZGV0YWlscy8xMjIwMjU0NzE%3D)

[机器学习——建立因果连系（传递熵）_时间序列计算传递熵需要满足什么性质-CSDN博客](https://blog.csdn.net/Alphoseven/article/details/103491897)

[在数据集上计算连续随机变量的信息熵和互信息--k-近邻估计方法_连续随机变量的熵-CSDN博客](https://blog.csdn.net/weixin_43992162/article/details/115207384)
