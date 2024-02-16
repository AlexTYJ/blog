形式：$\text{minimize}\ q(x_0,\cdots,x_m)\quad s.t.\ x_j\in\{0,1\},\ j=0,\cdots,m$，其中$q$是关于$x_j$的二次多项式

模型互化：变量代换    $x_j=\left\{\begin{array}{ll}0,&z_j=1,\\1,&z_j=-1,\end{array}\right.\quad j=0,\cdots,m$

+ Ising模型$(z_j\in\{1,-1\})$ $\to$ QUBO范式$(x_j\in\{0,1\})$
	令$z_j=1-2x_j$
+ QUBO范式 $\to$ Ising模型
	令$x_j=\dfrac{1-z_j}{2}$
