描述：判断一张图能否使用k种颜色对顶点着色

限制：

1. 每个顶点有且仅有一种颜色
2. 相连顶点颜色不同

QUBO范式建模：

+ 刻画：
	1. 着色：定义二进制变量$x_{jl}\in\{0,1\},x_{jl}=\left\{\begin{array}{ll}1,&\text{顶点}j\text{着色}l,\\0,&\text{其它}.&\end{array}\right.$$j=0,\cdots,m,\ l=0,\cdots,k-1$
	2. 唯一性：$\forall\text{顶点}j,\sum\limits_{l=0}^{k-1}x_{jl}=1.$
	3. 互斥性：$\forall\text{顶点}j,h,(j,h)\in E$，顶点$j,h$着色不同，即$\sum\limits_{l=0}^{k-1}x_{jl}x_{hl}=0.$
+ 有解问题$\to$最值问题：惩罚项
	将条件作为惩罚项放入目标式$0=0$中

$$
\begin{array}{rl}
\text{minimize}&\sum_\limits{j=0}^m\left(\sum_\limits{l=0}^{k-1}x_{jl}-1\right)^2+\sum_\limits{(j,h)\in E}\sum_\limits{l=0}^{k-1}x_{jl}x_{hl}\\
s.t.&x_{jl}\in\{0,1\},\quad j=0,\cdots,m,\ l=0,\cdots,k-1
\end{array}
$$

> 其中$\sum_{l=0}^{k-1}x_{jl}x_{hl}$恒非负，无需平方
> 优化目标为0，惩罚系数可任取（相当于无穷大） 

