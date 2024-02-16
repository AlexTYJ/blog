分类问题：询问“哪一个”
> 通常不区分硬类别(样本属于哪个类别)和软类别(样本属于每个类别的概率)：将硬类别当作软类别处理

分类数据表示：one-hot编码

+ 类别对应的分量设为1，其余分量设为0

网络架构：$\mathbf o=\mathbf {Wx}+\mathbf b$

![](https://zh.d2l.ai/_images/softmaxreg.svg)

+ 问题：输出无法直接作为概率使用
+ 解决：softmax
> softmax回归的输出层也是全连接层
> 对于d输入q输出的全连接层，开销为$O(dq)$


softmax函数：将输出$\hat y_j$转化为可视为属于类$j$的概率，选择$\mathop{\arg\max}\limits_jy_j$作为预测

+ 定义：$\mathbf{\hat y}=\text{softmax}(\mathbf o)\quad y_j=\dfrac{\exp(o_j)}{\sum_k\exp(o_k)}$
+ 性质：
	+ 归一化，非负性，可导
	+ $\mathop{\arg\max}\limits_j\hat y_j=\mathop{\arg\max}\limits_jo_j$
+ 优化：小批量样本标准化
	+ 设批量大小为$n$, $\mathbf X\in\mathbb R^{n\times d},\mathbf W\in\mathbb R^{d\times q},\mathbf b\in\mathbb R^{1\times q}$，$\mathbf{O=XW+b}$，$\hat{\mathbf Y}=\text{softmax}(\mathbf O)$
	+ 对$\mathbf O$的每一行，先对所有项进行幂运算，再求和标准化
> softmax回归是线性模型

损失函数：交叉熵损失函数

+ 熵：$H[P]=\sum\limits_j-P(j)\ln P(j)$

梯度：$\partial_{o_j}l(\mathbf y,\hat{\mathbf y})=\text{softmax}(\mathbf o)_j-y_j$，即模型分配的概率与实际发生的情况间的差异

+ 推导：

$$
\begin{array}{ll}
l(\mathbf y,\hat{\mathbf y})&=-\sum\limits_{j=1}^qy_j\ln\dfrac{\exp(o_j)}{\sum_{k=1}^q\exp(o_k)}\\
&=\sum\limits_{j=1}^qy_j\ln\sum\limits_{k=1}^q\exp(o_k)-\sum\limits_{j=1}^qy_jo_j\\
&=\ln\sum\limits_{k=1}^q\exp(o_k)-\sum\limits_{j=1}^qy_jo_j
\end{array}
$$

$$
\partial_{o_j}l(\mathbf y,\hat{\mathbf y})=\dfrac{\exp(o_j)}{\sum_{k=1}^q\exp(o_k)}-y_j=\text{softmax}(\mathbf o)_j-y_j
$$

预测：预测概率最高的类别作为输出类别

评估：精度

+ $\text{精度}=\dfrac{\text{正确预测数}}{\text{预测总数}}$
