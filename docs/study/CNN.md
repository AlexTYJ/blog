# CNN知识总结

## CNN的动机

不用考虑整个图片，只想考虑局部特征，我们引入了receptive field(感受野)。receptive field在图像处理领域一般为3*3，但是在其他的任务中可以被精心设计。比如，可以不连续，可以是奇形怪状的……

我们使用filter来提取特征。filter是可学习的。我们使用很多个filter来描述一个receptive field。经过一个卷积层后，**得到的输出的channel数=filter数**。一个filter就产生一个channel。

stride（步长）我们一般设置为1或2，这是因为我们希望有重叠（overlap），这样可以检测到全部区域。

如果超出范围，需要做padding。padding可以补0，也可以补其他的，可以被设计。一般上下左右都要padding。

经过卷积层后的输出我们称之为feature map。

假设输入形状为 $(n_h * n_w)$，卷积核形状为 $(k_h * k_w)$，总共添加了 $p_h$ 行和 $p_w$ 列的padding，垂直步幅为 $s_h$ ，水平步幅为 $s_w$ 时，输出形状为：

$$(output_h,output_w)=( \left\lfloor \frac{n_h+p_h-k_h}{s_h} \right\rfloor + 1 , \left\lfloor \frac{n_w+p_w-k_w}{s_w} \right\rfloor +1 )$$

特别注意，在调用pytorch的卷积的时候，padding的参数是tuple(元组)，就可以直接带入公式。如果是整数p，则代表 $p=0.5*p_h=0.5*p_w$ ，所以代入公式时p要先乘2

## Transposed CNN 转置卷积

### 动机
卷积层只会让矩阵越来越小。如何让矩阵变大？（有的时候要求保持分辨率输出）答：采用转置卷积

### 原理
首先，传统CNN可以表示为矩阵乘积形式。假设输入形状为 $(n_h * n_w)$，把它flatten变成 $((n_h+n_w) * 1)$ 的矩阵。则卷积可以用矩阵乘法形式写成 $$ WX=Y $$

此时$Y$的维度是小于$X$的。

注意这里的$W$并不是随意的矩阵，它需要满足一些条件（拥有着特定的构造），里面有特定位置的元素为0，其他位置是原来filter里面元素的重复排列。具体特征可以举个例子手推。

下面保持原来$W$的特征不变，把它转置，我们得到一个$W^T$

用$W^T$去左乘和$Y$一样形状的输入，可以得到和$X$一样形状的输出。但请注意，$W^TY \neq X$

如果我们还原回原来的卷积操作，可以发现：只要维持$W$的特征不变，那么在卷积层面上，这一步操作可以理解为：把输入的张量的每个元素作为权重乘以$W$，按步长排列后相同位置处相加。

总结：如果卷积将输入从(h,w)变为(h',w')，转置卷积在同样超参数下将(h',w')变为(h,w)。

这就是转置卷积的由来。

注：特别注意，由于这个时候我们的参数直接沿用的正常卷积，所以padding的意义变成了：输出最外面的一圈。

### 操作
具体操作时，我们需要想办法在卷积层面还原成和CNN一样的形式。我们通过补0来实现。具体方法为：在输入的相邻两行/列的中间分别添加 $s_h-1$ 行， $s_w-1$列0元素。在输入的上下总共添加 $2k_h-2-p_h$ 行， 左右总共 $2k_w-2-p_w$ 列。然后把卷积核上下左右翻转。

接下来做正常CNN一样的且stride=1，padding=0的卷积即可。


### 输出公式
假设输入形状为 $(n_h * n_w)$，卷积核形状为 $(k_h * k_w)$，padding为 $p_h$ 和 $p_w$ ，垂直步幅为 $s_h$ ，水平步幅为 $s_w$ 时：

1. 从原理上直接计算，可以得到输出为 $((n_h-1)s_h+k_h-p_h , (k_h-1)s_h+n_h-p_w)$。注意需要直接减去padding的大小（没什么实际意义，就为了参数统一）。

2. 从实际操作上来计算，等价于输入为 

$$
\begin{align*}
(n'_h,n'_w) &= (n_h + (n_h-1)(s_h-1)+2(k_h-p_h-1) , n_w + (n_w-1)(s_w-1)+2(k_w-p_w-1)) \\
&= (n_h*s_h-s_h+2k_h-2p_h-1 ,n_w*s_w-s_w+2k_w-2p_w-1) 
\end{align*}
$$ 

和将步长为1填充为0带入传统CNN的公式，得到输出为

$$ ((n_h-1)s_h+k_h-p_h,(n_w-1)s_w+k_w-p_w) $$

3. 直接把原始式子的 $output_h$ 和 $n_h$， $output_w$ 和$n_w$对调。直接把取整去掉因为反方向不存在不整除的问题。得到结果为

$$ ((n_h-1)s_h+k_h-p_h,(n_w-1)s_w+k_w-p_w) $$


可以看到三者答案相同。

### 接口
torch.nn.ConvTranspose2d参数：

- in_channels(int):输入大小
- out_channels(int):输出大小
- kernel_size(int or tuple):卷积核大小
- stride(int or tuple,optional):步长。默认1。
- padding(int or tuple,optional):填充，注意可能为整数可能为元组，定义同传统CNN（公式整数的话公式中p要乘2）。默认0。
- output_padding(int or tuple,optional):输出加的额外的padding，默认为0。
- groups(int,optional):是否使用分组卷积。默认1（传统卷积）。
- bias(bool,optinal):是否加偏置，默认为True
- dilation(int or tuple,optional):是否使用空洞卷积，默认为1（普通卷积）