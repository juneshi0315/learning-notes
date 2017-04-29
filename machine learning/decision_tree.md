<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>
<script type="text/javascript" async src="path-to-mathjax/MathJax.js?config=TeX-AMS_CHTML"></script>

# 决策树

## 基本概念

1. 熵
  
  表示随机变量的不确定程度。熵越大，随机变量不确定性就越大，其信息量就越大。
  设X是一个离散随机变量（如果是连续随机变量？），其概率分布为
  $$
      P(X=x_i)=p_i,　i=1,2,...,n
  $$
  则随机变量的熵定义为
  $$
  H(X)=-\sum_{i=1}^n p_i\log p_i
  $$
  可看作$$$-\log P(X=x_i)$$$的期望。
  
2. 条件熵
  
  $H(Y|X)$表示在已知随机变量$X$的条件下，随机变量$Y$的不确定性，定义为$X$给定的条件下$Y$的条件概率分布的熵对$X$的数学期望。
  $$
  \begin{align}
  H(Y|X)&=\sum_{i=1}^n P(X=x_i)\cdot H(Y|X=x_i)\\
  &=\sum_{i=1}^nP(X=x_i)\cdot (-\sum_{j=1}^n P(Y=y_j|X=x_i)\log P(Y=y_j|X=x_i))\\
  &=-\sum_{i=1}^n \sum_{j=1}^n P(X=x_i, Y=y_j)\cdot \log P(Y=y_j|X=x_i)\\
  &=-\sum_{i=1}^n \sum_{j=1}^n P(X=x_i, Y=y_j)\cdot \log \frac {P(X=x_i, Y=y_j)}{P(X=x_i)})\\
  &=-\sum_{i=1}^n \sum_{j=1}^n P(X=x_i, Y=y_j)\cdot \log P(X=x_i,Y=y_j)+\sum_{i=1}^n \sum_{j=1}^n P(X=x_i, Y=y_j)\cdot \log P(X=x_i)\\
  &=-\sum_{i=1}^n \sum_{j=1}^n P(X=x_i, Y=y_j)\cdot \log P(X=x_i,Y=y_j)+\sum_{i=1}^n P(X=x_i)\cdot \log P(X=x_i)\\
  &=H(X,Y)-H(X)
  \end{align}
  $$
  条件熵满足$H(X,Y)=H(X)+H(Y|X)=H(Y)+H(X|Y)$，而条件概率满足$P(X,Y)=P(X)\cdot P(Y|X)=P(Y)\cdot P(X|Y)$，因为熵是概率的对数形式。
  *当熵和条件熵由数据估计得到时，熵和条件熵分别称为**经验熵**和**经验条件熵***
  
3. 信息增益
  
  特征$A$对训练数据集$D$的信息增益$g(D,A)$，定义为集合$D$的经验熵$H(D)$（随机变量为样本的**类别**）与特征$A$给定条件下$D$的经验条件熵$H(D|A)$之差
  $$
  g(D,A)=H(D)-H(D|A)
  $$
  经验熵$H(D)$表示对数据集$D$进行分类的不确定性，
  经验条件熵$H(D|A)$表示在特征$A$给定的条件下对数据集$D$进行分类的不确定性，
  那么他们的差，即信息增益，表示由于特征$A$而使得数据集$D$的分类的不确定性减少的程度
  **缺陷**：以信息增益作为划分训练数据集的特征，存在偏向于选择**取值较多的特征**的问题。（考虑极端情况，若$A$将$D$中的每个样本作为一个子集，则$H(D|A)=0$，则该特征对应的信息增益最大）
  
4. 信息增益比
  
  特征$A$对训练数据集$D$的信息增益比$g_r(D,A)$定义为其信息增益$g(D,A)$与**训练数据集$D$关于特征$A$的取值的熵$H_A(D)$**之比
  其中，$H_A(D)=-\sum_{i=1}^n P(A=a_i)\log P(A=a_i)$，$n$为特征$A$的取值个数，$P(A=a_i)$表示数据集中特征$A$取值为$a_i$的样本频率。
  
5. 基尼指数
  
  分类问题中，假设有$K$个类，样本点属于第$k$类的概率为$p_k$，则概率分布的基尼指数定义为
  $$
  Gini(p)=\sum_{k=1}^K p_k(1-p_k)=1-\sum_{k=1}^K p_k^2
  $$
  对于给定样本集合$D$，其基尼指数为
  $$
  Gini(D)=1-\sum_{k=1}^K(\frac {|C_k|}{|D})^2
  $$
  其中，$C_k$是$D$中属于第$k$类的样本子集。

## ID3
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default">
$$
Gini(D)=1-\sum_{k=1}^K(\frac {|C_k|}{|D})^2
$$
</script>

## C4.5


## CART

