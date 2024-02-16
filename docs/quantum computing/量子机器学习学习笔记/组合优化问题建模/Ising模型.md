背景：统计物理学中描述铁磁系统的模型，每个阵点具有上下两种自旋方向（记做1,-1），点阵常以格状排列

![Ising model|350](https://s2.loli.net/2023/08/14/JDhPgqyjRHotmQk.png)

哈密顿算符：

$$
-\sum_{j,k}J_{j,k}z_jz_k-\sum_jh_jz_j
$$

> 其中$J_{j,k}$表示粒子$j,k$的相互作用（一般仅相邻粒子具有相互作用），$h_j$表示外部磁场对粒子$j$的作用

特例：当$J_{j,k}=-1,\ h_j=0$时，退化为Max-Cut问题
