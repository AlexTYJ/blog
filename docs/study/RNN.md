# RNN进阶知识总结
## RNN BP反传推导
RNN基本公式为：

$$ 
\begin{split}\begin{aligned}
\mathbf{h}_t &= \mathbf{W}_{hx} \mathbf{x}_t + \mathbf{W}_{hh} \mathbf{h}_{t-1},\\
\mathbf{o}_t &= \mathbf{W}_{qh} \mathbf{h}_{t},\\
L &= \frac{1}{T} \sum_{t=1}^T l(\mathbf{o}_t, y_t) 
\end{aligned}\end{split}
$$

其中：

$$ \mathbf{W}_{hx} \in \mathbb{R}^{h \times d} , \mathbf{W}_{hh} \in \mathbb{R}^{h \times h} , \mathbf{W}_{qh} \in \mathbb{R}^{q \times h} $$


接下来求偏导，先求关于 $\mathbf{W}_{qh}$ 的，比较简单：

首先计算中间变量：

$$
\frac{\partial L}{\partial \mathbf{o}_t} =  \frac{\partial l (\mathbf{o}_t, y_t)}{T \cdot \partial \mathbf{o}_t} \in \mathbb{R}^q
$$

所以：

$$
\frac{\partial L}{\partial \mathbf{W}_{qh}}
= \sum_{t=1}^T \text{prod}\left(\frac{\partial L}{\partial \mathbf{o}_t}, \frac{\partial \mathbf{o}_t}{\partial \mathbf{W}_{qh}}\right)
= \sum_{t=1}^T \frac{\partial L}{\partial \mathbf{o}_t} \mathbf{h}_t^\top
= \sum_{t=1}^T \frac{\partial l (\mathbf{o}_t, y_t)}{T \cdot \partial \mathbf{o}_t} \mathbf{h}_t^\top
$$

由公式可以全部直接求出。

下面求中间变量 $\partial L/\partial \mathbf{h}_t \in \mathbb{R}^h$ 。为了求这个，我们先从最后时间T开始求起:

$$
\frac{\partial L}{\partial \mathbf{h}_T} = \text{prod}\left(\frac{\partial L}{\partial \mathbf{o}_T}, \frac{\partial \mathbf{o}_T}{\partial \mathbf{h}_T} \right) = \mathbf{W}_{qh}^\top \frac{\partial L}{\partial \mathbf{o}_T}
$$

由于目标函数 $L$ 依赖于 $\mathbf{h}_t$，而 $\mathbf{h}_t$ 又依赖于 $\mathbf{h}_{t+1}$ 和 $\mathbf{o}_t$，所以我们由链式法则：

$$
\frac{\partial L}{\partial \mathbf{h}_t} = \text{prod}\left(\frac{\partial L}{\partial \mathbf{h}_{t+1}}, \frac{\partial \mathbf{h}_{t+1}}{\partial \mathbf{h}_t} \right) + \text{prod}\left(\frac{\partial L}{\partial \mathbf{o}_t}, \frac{\partial \mathbf{o}_t}{\partial \mathbf{h}_t} \right) = \mathbf{W}_{hh}^\top \frac{\partial L}{\partial \mathbf{h}_{t+1}} + \mathbf{W}_{qh}^\top \frac{\partial L}{\partial \mathbf{o}_t}
$$

进一步递归分析，得：

$$
\frac{\partial L}{\partial \mathbf{h}_t}= \sum_{i=t}^T {\left(\mathbf{W}_{hh}^\top\right)}^{T-i} \mathbf{W}_{qh}^\top \frac{\partial L}{\partial \mathbf{o}_{T+t-i}}
$$

接下来就可以计算关于 $\mathbf{W}_{hx}$ 和 $\mathbf{W}_{hh}$ 的偏导了，得：

$$
\begin{split}\begin{aligned}
\frac{\partial L}{\partial \mathbf{W}_{hx}}
&= \sum_{t=1}^T \text{prod}\left(\frac{\partial L}{\partial \mathbf{h}_t}, \frac{\partial \mathbf{h}_t}{\partial \mathbf{W}_{hx}}\right)
= \sum_{t=1}^T \frac{\partial L}{\partial \mathbf{h}_t} \mathbf{x}_t^\top,\\
\frac{\partial L}{\partial \mathbf{W}_{hh}}
&= \sum_{t=1}^T \text{prod}\left(\frac{\partial L}{\partial \mathbf{h}_t}, \frac{\partial \mathbf{h}_t}{\partial \mathbf{W}_{hh}}\right)
= \sum_{t=1}^T \frac{\partial L}{\partial \mathbf{h}_t} \mathbf{h}_{t-1}^\top,
\end{aligned}\end{split}
$$

其中 $\frac{\partial L}{\partial \mathbf{h}_t}$ 需要带入上面

我们发现，$\frac{\partial L}{\partial \mathbf{h}_t}$ 中 $\mathbf{W}_{hh}^\top$ 的**幂非常大**。在这个幂中，小于1的特征值将会消失，大于1的特征值将会发散。这在数值上是不稳定的，表现形式为梯度消失或梯度爆炸。

在实际应用中，采用常规截断或者随机截断。然而，随机截断在实际应用中并不好。

下面是三种方法的示意图：

![truncated-bptt](./truncated-bptt.svg "truncated-bptt")


此外，我们还可以通过“梯度裁剪”的方法来限制梯度 $\mathbf{g}$ 不超过 $\theta$ ：
$$ \mathbf{g} \leftarrow \min\left(1, \frac{\theta}{\|\mathbf{g}\|}\right) \mathbf{g} $$