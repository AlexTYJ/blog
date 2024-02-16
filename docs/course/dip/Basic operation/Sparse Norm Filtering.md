思路：

+ 均值滤波：
$$
\min_{l_i^{\text{new}}}\sum_{j\in N_i}(I_i^{\text{new}}-I_j)^2
$$

+ 利用稀疏范数进行保边滤波：

$$
\min_{l_i^{\text{new}}}\sum_{j\in N_i}|I_i^{\text{new}}-I_j|^p,0<p\leqslant2
$$
