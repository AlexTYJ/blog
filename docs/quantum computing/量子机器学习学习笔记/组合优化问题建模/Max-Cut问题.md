描述：将图的顶点划分为两个集合，使得顶点落在不同集合中的边数最多

Ising模型建模：设变量$z_i$对应顶点$i=0,\cdots,n-1$且$z_i\in\{1,-1\}$表示落在不同的集合中
当顶点$j,k$落在同一集合中时，$z_jz_k=1$；反之$z_jz_k=-1$.
故问题可写作

$$
\text{minimize}\ \sum_{(j,k)\in E}z_jz_k\quad s.t.\ z_j\in\{-1,1\},\ j=0,\cdots,n-1
$$
