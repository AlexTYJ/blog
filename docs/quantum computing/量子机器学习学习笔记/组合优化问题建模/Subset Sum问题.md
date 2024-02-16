描述：给定整数集合$S$和整数$T$，问是否存在$S$的子集，使得其元素之和为$T$

QUBO范式建模：设二进制变量$x_j\in\{0,1\}$对应是否选取第$j$个元素$(j=0,\cdots,m)$，给定$S=\{a_0,\cdots,a_m\},\ T$，构造$c(x_0,x_1,\cdots,x_m)=(a_0x_0+a_1x_1+\cdots+a_mx_m-T)^2$，则Subset Sum问题有解当且仅当$\exists x_j,\ j=0,\cdots,m\quad s.t.\ c(x_0,x_1,\cdots,x_m)=0$.
由于$c(x_0,x_1,\cdots,x_m)$恒正，故原问题可转化为求最小值：Subset Sum问题有解当且仅当$c(x_0,x_1,\cdots,x_m)$最小值为0.
而最值问题可写作

$$
\text{minimize}\ (a_0x_0+a_1x_1+\cdots+a_mx_m-T)^2\quad s.t.\ x_j\in\{0,1\},\ j=0,\cdots,m
$$
