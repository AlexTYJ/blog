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
联合概率密度函数的链式法则：$p(x_{1},x_{2},...,x_{n})=p(x_{1})p(x_{2}|x_{1},x_{2})p(x_{3}|x_{1},x_{2})...p(x_{n}|x_{1},...,x_{n-1})$

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

Let p(x),q(x),x∈X be two PMF, then $D[p||q]>=0$, with equality if and only if p(x)=q(x), $\forall x ∈ X$

#### Theorem 2.6.4

Let x∈X, then $H(x)\leq log|X|$ with equality iff X has a uniform distribution over X

#### Theorem 2.6.5 (conditioning reduces entropy)
$H(X|Y)\leq H(x)$

#### Theorem 2.6.6
$H(X_{1},X_{2})\leq H(x_{1})+H(x_{2})$