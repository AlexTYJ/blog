元素：

+ 输入：$p_i$，带有噪声$n_i$
+ 输出：$q_i=p_i-n_i$
+ guide：$I$

原理：

$$
\nabla q_i=a\nabla I_i
$$

$$
q_i=aI_i+b
$$

形式化：

$$
\min_{(a,b)}\sum_i(aI_i+b-p_i)^2+\epsilon a^2
$$

其中$\epsilon a^2$为正则项；上式即噪声最小。

求解最优化问题：Lagrange

$$
a=\dfrac{\text{cov}(I,p)}{\text{var}(I)+\epsilon}
$$

$$
b=\bar p-a\bar I
$$

优化：利用重叠窗口

+ 窗口定义：

$$
\begin{array}{l}
a_k=\dfrac{\text{cov}_k(I,p)}{\text{var}_k(I)+\epsilon}\\
b_k=\bar{p_k}-a\bar{I_k}\\
q_i=\dfrac{1}{|\omega|}\sum\limits_{k|i\in\omega_k}(a_kI_i+b_k)=\bar{a_i}I_i+\bar{b_i}
\end{array}
$$

参数影响：

+ $I$：当$\text{var}(I)<\!<\epsilon$时，$a\approx0,b\approx\bar p\Rightarrow q_i\approx\bar{\bar p}$
+ $r$：影响band-width
+ $\epsilon$：影响保边（当$I$存在阶梯时，输出也存在阶梯）

复杂度：$O(1)$

应用：

+ 细节增强（无梯度逆转）
+ 图像压缩
+ 图像去噪
+ 去雾：$\epsilon\to0$
+ 边缘提取
