# 优化算法
## Momentum

储存了上一时刻的动量信息。 $\mathbf{v}_t$ 即为动量

$$
\begin{split}\begin{aligned}
\mathbf{v}_t &\leftarrow \beta \mathbf{v}_{t-1} + \mathbf{g}_{t, t-1}, \\
\mathbf{x}_t &\leftarrow \mathbf{x}_{t-1} - \eta_t \mathbf{v}_t.
\end{aligned}\end{split}
$$

$\mathbf{v}_t$ 可以递归计算，得到：

$$
\begin{aligned}
\mathbf{v}_t = \beta^2 \mathbf{v}_{t-2} + \beta \mathbf{g}_{t-1, t-2} + \mathbf{g}_{t, t-1}
= \ldots, = \sum_{\tau = 0}^{t-1} \beta^{\tau} \mathbf{g}_{t-\tau, t-\tau-1}.
\end{aligned}
$$

也就是说，Momentum方法将瞬时梯度替换为多个“过去”梯度的平均值。

## AdaGrad

我们希望消除不同特征量纲的影响，稀疏特征和常见特征需要不同的学习率来达到极值点。

设计新的向量 $s_t$ ，累计了过去的梯度方差。

$$
\begin{split}\begin{aligned}
    \mathbf{g}_t & = \partial_{\mathbf{w}} l(y_t, f(\mathbf{x}_t, \mathbf{w})), \\
    \mathbf{s}_t & = \mathbf{s}_{t-1} + \mathbf{g}_t^2, \\
    \mathbf{w}_t & = \mathbf{w}_{t-1} - \frac{\eta}{\sqrt{\mathbf{s}_t + \epsilon}} \cdot \mathbf{g}_t.
\end{aligned}\end{split}
$$

## RMSProp
AdaGrad中学习率依时间步$t$,  $O(t^{-1/2})$ 量级降低，$s_t$ 没有约束，将持续增长。一种改进方法如下：

将 $s_t$ 修改为：

$$
\begin{split}\begin{aligned}
\mathbf{s}_t & = (1 - \gamma) \mathbf{g}_t^2 + \gamma \mathbf{s}_{t-1} \\
& = (1 - \gamma) \left(\mathbf{g}_t^2 + \gamma \mathbf{g}_{t-1}^2 + \gamma^2 \mathbf{g}_{t-2} + \ldots, \right).
\end{aligned}\end{split}
$$

其余不变：

$$
\begin{split}\begin{aligned}
    \mathbf{s}_t & \leftarrow \gamma \mathbf{s}_{t-1} + (1 - \gamma) \mathbf{g}_t^2, \\
    \mathbf{x}_t & \leftarrow \mathbf{x}_{t-1} - \frac{\eta}{\sqrt{\mathbf{s}_t + \epsilon}} \odot \mathbf{g}_t.
\end{aligned}\end{split}
$$

## Adadelta

$$
\begin{aligned}
    \mathbf{s}_t & = \rho \mathbf{s}_{t-1} + (1 - \rho) \mathbf{g}_t^2.
\end{aligned}
$$

$$
\begin{split}\begin{aligned}
    \mathbf{g}_t' & = \frac{\sqrt{\Delta\mathbf{x}_{t-1} + \epsilon}}{\sqrt{{\mathbf{s}_t + \epsilon}}} \odot \mathbf{g}_t, \\
\end{aligned}\end{split}
$$

$$
\begin{split}\begin{aligned}
    \mathbf{x}_t  & = \mathbf{x}_{t-1} - \mathbf{g}_t'. \\
\end{aligned}\end{split}
$$

其中 $\Delta \mathbf{x}_{t-1}$ 是重新缩放梯度的平方 $\mathbf{g}_t'$ 的泄漏平均值。我们将 $\Delta \mathbf{x}_{0}$ 初始化为0，然后在每个步骤中使用 $\mathbf{g}_t'$ 更新它，即

$$
\begin{aligned}
    \Delta \mathbf{x}_t & = \rho \Delta\mathbf{x}_{t-1} + (1 - \rho) {\mathbf{g}_t'}^2,
\end{aligned}
$$

$\epsilon$ （例如 $10^{-5}$这样的小值）是为了保持数字稳定性而加入的

## Adam
Adam算法结合了Momentum和RMSProp的工作。

使用指数加权平均来维护梯度的动量和二次矩，并在初始时使用标准化公式：

$$
\begin{split}\begin{aligned}
    \mathbf{v}_t & \leftarrow \beta_1 \mathbf{v}_{t-1} + (1 - \beta_1) \mathbf{g}_t, \\
    \mathbf{s}_t & \leftarrow \beta_2 \mathbf{s}_{t-1} + (1 - \beta_2) \mathbf{g}_t^2.
\end{aligned}\end{split}
$$