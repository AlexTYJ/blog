# 信息论

## 第一章 绪论

&emsp;&emsp;本课程是中国科学院大学人工智能学院开设的专业选修课，使用的教材是 Thomas M.Cove 所著的《信息论基础》，要求的前序课程为**概率与统计**，**微积分**与**线性代数**。

---

## 第二章 熵和互信息基础

### 2.1 Entropy

&emsp;&emsp;定义离散型随机变量 X~P，其概率密度函数为 p(x)，则我们可以定义熵(Entropy):

$$
H_{b}(x)\stackrel{def}{=}-\sum_{x}p(x)log_b(p(x))
$$

&emsp;&emsp;在不加额外说明的情况下，我们默认 b=2 并将下标忽略，也即$H[x]=H_{2}[x]$。我们将 b=2 时，H[x]的单位称为 bit.

&emsp;&emsp;此外，当 b=e，即自然对数时，H[x]的单位称为 nat.

**Remark:**

1. 所谓的 H[x]并不是关于 x 的函数，而是关于概率密度函数 p 的函数。严格来说应该写作 H[p].
2. H[x]可以视作$-E_{X \sim P}(logp(x))$，即 logp(x)的期望再取反

---

### 2.2 Joint entropy & conditional entropy

&emsp;&emsp;类似地，我们可以定义 Joint Entropy:

$$
H[x,y]\stackrel{def}{=}-E_{X,Y\sim p_{X,Y}}logp(x,y)=-\sum_{X,Y}p(x,y)logp(x,y)
$$

&emsp;&emsp;与 Conditional Entropy:

$$
H[x|y]\stackrel{def}{=}-E_{X,Y\sim p_{X,Y}}logp(x|y)=-\sum_{X,Y}p(x,y)logp(x|y)
$$

&emsp;&emsp;它们之间的关系可以用如下的图表示：
![图片1](p1.jpeg)

---

### 2.3 mutual information

&emsp;&emsp;中间的 mutual information 我们定义为:

$$
I[x,y]\stackrel{def}{=}\sum_{X,Y}p(x,y)log\frac{p(x,y)}{p(x)p(y)}
$$

&emsp;&emsp;可以证明，I(x,y)也可以被表示为

$$
I(X,Y)=H[x]-H[x|y]=H[y]-H[y|x]=H[x,y]-H[x|y]-H[y|x]
$$

Conditional mutual information：

$$ I(X,Y|Z)=H(X|Z)-H(X|Y,Z)=\sum_{x,y,z}log\frac{p(x,y|z)}{p(x|z)p(y|z)}=E_{Z\sim p(z)}I(X,Y|Z=z)$$

---

### 2.4 K-L diverence(relative entropy)
定义: 
$$ D[p||q]=\sum_{X}p(x)log\frac{p(x)}{q(x)}=E_{X\sim P}log\frac{p(x)}{q(x)}$$ 
用以描述p(x)和q(x)的距离

补充定义：$0log\frac{0}{0}=0,0log\frac{0}{q}=0,plog\frac{p}{0}=\infty$ , for $p>0$

性质：

1. $D[p||q]\geq 0$ 
2. $D[p||q]=0 \iff p(x)=q(x),x∈X$
3. $\exists x∈X_{p}, p(x)>0&emsp;and&emsp;q(x)=0&emsp;then&emsp;D[p||q]=\infty$ 

注：可以导出互信息的另一种定义方式：$I[x,y]=D[p(x,y)||p(x)p(y)]$

定义：conditon K_L divergence:
$$ D[p(Y|X)|| q(Y|X)]=\sum_{x}p(x)D[p(Y|X=x)||q(Y|X=x)]=\sum_{x}p(x)\sum_{y}p(y|x)log\frac{p(y|x)}{q(y|x)}=E_{x,y\sim p(x,y)}log\frac{p(y|x)}{q(y|x)} $$

---

### 2.5 chainrules
联合概率密度函数的链式法则：$p(x_{1},x_{2},...,x_{n})=p(x_{1})p(x_{2}|x_{1})p(x_{3}|x_{1},x_{2})...p(x_{n}|x_{1},...,x_{n-1})$

熵的链式法则：

Let $X_{1},X_{2},...,X_{n}$ be drawn according to $p(x_{1},x_{2},...,x_{n})$, then:

$$H (X_{1},X_{2},...,X_{n})=H(x_{1})+H(X_{2}|X_{1})+H(X_{3}|X_{1},X_{2})+...+H(X_{n}|X_{1},X_{2},...,X_{n-1})$$

互信息的链式法则：

$$I(X_{1:n};Y)=I(X_{1};Y) + I(X_{2};Y|X_{1}) + I(X_{3};Y|X_{1},X_{2})+...+I(X_{n};Y|X_{1:n-1})$$

KL散度的链式法则：
$$ D[p(Y|X)|| q(Y|X)]=D[p(X)||q(X)] + D[p(Y|X)||q(Y|X)] $$ 

---

### 2.6 Jensen inequality and proofs of properties about D,H,I
#### Theorem 2.6.3 (information inequality) 

Let p(x),q(x),x∈X be two PMF, then $D[p||q]>=0$, 等号成立当且仅当p(x)=q(x), $\forall x ∈ X$

#### Theorem 2.6.4

Let x∈X, then $H(x)\leq log|X|$ 等号成立当且仅当X服从均匀分布

#### Theorem 2.6.5 (conditioning reduces entropy)
$H(X|Y)\leq H(x)$

#### Theorem 2.6.6
$H(X_{1},X_{2})\leq H(x_{1})+H(x_{2})$
证明：$H(x_{1},x_{2})=H(x_{1})+H(x_{2}|x_{1})\leq H(x_{1})+H(x_{2})$

推广：$H(x_{1},x_{2},...,x_{n})\leq \sum_{i=1}^{n}H(x_{i})$

--- 

### 2.7 log-sum inequality
#### Theorem 2.7.1
对于$a_{i},b_{i}>0,i=1,2,…,n,\sum_{i=1}^{n}a_{i}log\frac{a_{i}}{b_{i}}\leq(\sum_{i=1}^{n})log\frac{\sum{i=1}^{n}a_{i}}{\sum{i=1}^{n}b_{i}}$

证明见课堂笔记第13页，思路：构造f(x)=xlogx，这是一个下凸函数。令$x=\frac{a_{i}}{b_{i}}$，再利用Jensen不等式。

通过这个不等式可以轻松证明定理2.6.3

#### Theorem 2.7.2 convexity of KL-divergence
对于两组PMFs $D[\lambda_{1}p_{1}+\lambda_{2}p_{2}||\lambda_{1}q_{1}+\lambda_{2}q_{2}]\leq \lambda_{1}D[p_{1}||q_{1}]+\lambda_{2}D[p_{2},q_{2}]$

证明：见课堂笔记14页，主要利用定理2.7.1

#### Theorem 2.7.3 concavity of entropy

H[p]是关于p的下凸函数

证明：H[p]=log|X|-D[p||u], 其中$u(x)=\frac{1}{|x|}$ 是X上的均匀分布

#### Theorem 2.7.4 convexity/concavity of mutual information

### 2.8 Diffential entropy
在这一章中，我们将熵的概念延拓，从离散延拓至连续。

一些定义：

1. X为连续变量
2. 分布函数Cumulative distribution function   $F(x)=P_{r}(X\leq x)$
3. Probability density function(PDF) $f(x)=\frac{d}{dx}F(x)$
4. Support set S of X: $\{x|f(x)>0\}$

定义：Diffential entropy h(x) of a continous random variable X
$$
h(x)\stackrel{def}{=}-\int_{S}f(x)logf(x)dx 
$$
where S is the support set of X

类似的，h(x)也可以被写作h[f]，被看做f(x)的函数

#### Theorem 2.8.1 translation invariant
设X是一个连续随机变量，C是一个常数，则h(X+C)=h(X)

#### Theorem 2.8.2 scaling changes the entropy
设X是一个连续随机变量，a是一个常数，则h(aX)=h(X)+loga

更一般地，h(AX)=h(X)+log(|det(A)|)

### 2.9 Joint and Conditional differential entropy
定义：一系列随机变量$X_{1},X_{2},...,X_{n}$的微分熵为$h(X_{1},X_{2},...,X{n})=-\int f(x^{n}logf(x^{n}))$，其中$f(x^{n})$是n维随机向量$x^{n}$的概率密度函数

定义：条件微分熵$h(X|Y)=-\int f(x,y)logf(x|y)dxdy = -E_{x,y~f(x,y)}logf(x|y)$

可以推出，h(X|Y)=h(X,Y)-h(Y)

### 2.10 Relative entropy (KL divergence) and mutual information
定义：Relative entropy (KL divergence) $D[f||g]=\int f(x)log\frac{f(x)}{g(x)} = E_{x\sim f}log\frac{f(x)}{g(x)}$

约定：$0log\frac{0}{0}=0$

定义：互信息$I(X;Y)=\int f(x,y)log\frac{f(x,y)}{f(x)f(y)}dxdy = E_{x,y \sim f(x,y)}log\frac{f(x,y)}{f(x)f(y)}$

#### Theorem
$$ D[f||g]\geq 0 with equality iff f=g almost everywhere $$

推论：
1. $ I(X,Y) \geq 0 $
2. $ h(X|Y) \leq h(X) $

#### chain rule
$h(X_{1},X_{2},...,X_{n})=h(X_{1})+h(X_{2}|X_{1})+h(X_{3}|X_{1},X_{2})+...+h(X_{n}|X_{1},X_{2},...,X_{n-1})$

推论：$h(X_{1},X_{2},...,X_{n}) \leq \sum_{i=1}^{n}h(X_{i})$

### 2.11 Data processing inequalitity
