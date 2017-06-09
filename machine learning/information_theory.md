## 信息论基础

### 熵

表示随机变量的不确定程度。熵越大，随机变量不确定性就越大，其信息量就越大。
设X是一个离散随机变量（如果是连续随机变量，熵无穷大，只能计算相对熵），其概率分布为
$$
P(X=x_i)=p_i,　i=1,2,...,n
$$
则随机变量的熵定义为
$$
H(X)=-\sum_{i} p_i\log p_i
$$
可看作随机变量负对数$$-\log P(X=x_i)$$的期望。

### 条件熵

$H(Y|X)$表示在已知随机变量$X$的条件下，随机变量$Y$的不确定性，定义为$X$给定的条件下$Y$的条件概率分布的熵对$X$的数学期望，即$X$给定的条件下$Y$的平均信息量。
$$
\begin{align}
H(Y|X)&=\sum_{x} P(X=x)\cdot H(Y|X=x) \\
&=\sum_{x} P(X=x)\cdot (-\sum_{y} P(Y=y|X=x)\log P(Y=y|X=x)) \\
&=-\sum_{x} \sum_{y} P(X=x, Y=y) \cdot \log P(Y=y|X=x) \\
&=-\sum_{x} \sum_{y} P(X=x, Y=y) \cdot \log \frac {P(X=x, Y=y)}{P(X=x)}) \\
&=-\sum_{x} \sum_{y} P(X=x, Y=y) \cdot \log P(X=x,Y=y)+\sum_{x} \sum_{y} P(X=x, Y=y)\cdot \log P(X=x) \\
&=-\sum_{x} \sum_{y} P(X=x, Y=y) \cdot \log P(X=x,Y=y)+\sum_{x} P(X=x)\cdot \log P(X=x )\\
&=H(X,Y)-H(X)
\end{align}
$$
条件熵满足$H(X,Y)=H(X)+H(Y|X)=H(Y)+H(X|Y)$，类似地，条件概率满足$P(X,Y)=P(X)\cdot P(Y|X)=P(Y)\cdot P(X|Y)$，因为熵是概率的对数形式。
当熵和条件熵由数据估计得到时，熵和条件熵分别称为**经验熵**和**经验条件熵**

### 互信息

互信息表示随机变量间**相互依赖的程度**(即相关性，与**相关系数**的区别？)。两个离散随机变量$X$和$Y$的互信息定义为：
$$
I(X;Y)=\sum_{y} \sum_{x} p(x, y) \log \frac{p(x,y)}{p(x) \cdot p(y)}
$$
连续随机变量互信息将求和替换为积分即可。

互信息又可以等价地表示为(参照下图理解)
$$
\begin{align}
I(X;Y) &= H(X) - H(X|Y) \\
&= H(Y) - H(Y|X) \\
&= H(X) + H(Y) -H(X,Y) \\
&= H(X,Y) -H(X|Y) - H(Y|X)
\end{align}
$$
即互信息可理解为已知$Y$的前提下，为消除$X$的不确定性所提供的信息量。

此外，互信息具有非负性，对称性；$0 \le I(X;Y) \le \min (H(X), H(Y))$；当$X$和$Y$独立时，$I(X;Y)=0$；

![img](http://image.sciencenet.cn/album/201607/07/090617u7nu8paman1tjm5s.jpg)

### 相对熵/交叉熵/KL散度(Relative Entropy/Cross Entropy/Kullback-Leibler Divergence)

用来衡量两个取值为正的函数的相似性，定义如下
$$
KL(f(x) || g(x)) = \sum_{x \in X} f(x) \cdot \log \frac{f(x)}{g(x)}
$$
