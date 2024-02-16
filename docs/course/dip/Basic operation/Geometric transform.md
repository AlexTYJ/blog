概念：利用变换函数改变图像中像素的位置，从而产生新图像的过程
> 几何变换不改变像素值，而是改变像素所在的位置

变换：

$$
g(x,y)=f(x',y')=f[a(x,y),b(x,y)]
$$

$$
\left\{
\begin{array}{l}
x'=a(x,y)\\
y'=b(x,y)
\end{array}
\right.
$$

分类：

+ 简单变换——变换过程（各个像素变换前后的位置）以及变换参数可知时的变换，如图像的平移、镜像、转置、旋转、缩放、错切变换等
+ 一般变换——变换过程不是一目了然，变换参数难以测量时的变换。通常情况下，对图像畸变进行校正时，需要用到较为复杂的变换公式

平移变换：将图像沿水平和竖直方向移动，从而产生新图像的过程

$$
\left\{
\begin{array}{l}
x'=x+x_0\\
y'=y+y_0
\end{array}
\right.
$$

$$
\begin{bmatrix}
x'\\
y'\\
1
\end{bmatrix}=
\begin{bmatrix}
1&0&x_0\\
0&1&y_0\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\
y\\
1
\end{bmatrix}
$$

> 移动后，画布延展，保留原空白；
> 平移后的景物与原图像相同，但“画布”一定是扩大了，否则就会丢失信息

镜像变换：绕x轴或y轴翻转，从而产生与原图像对称的新图像的过程

绕x轴：

$$
\left\{
\begin{array}{l}
x'=x\\
y=-y
\end{array}
\right.
$$

绕y轴：

$$
\left\{
\begin{array}{l}
x'=-x\\
y=y
\end{array}
\right.
$$

$$
\begin{bmatrix}
x'\\ y'\\1
\end{bmatrix}=
\begin{bmatrix}
s_x&0&0\\0&s_y&1\\0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

$s_x=1,s_y=-1$绕$x$轴，$s_x=-1,s_y=1$绕$y$轴.

旋转变换：绕原点旋转$\theta$角，得到新图像的过程

$$
\left\{
\begin{array}{l}
x'=x\cos\theta-y\sin\theta\\
y'=x\sin\theta+y\cos\theta
\end{array}
\right.
$$

$$
\begin{bmatrix}
x'\\y'\\1
\end{bmatrix}=
\begin{bmatrix}
\cos\theta&-\sin\theta&0\\
\sin\theta&\cos\theta&0\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

问题：图像经过旋转变换以后，新图像中会出现许多空洞 （浮点数被舍弃）

解决：插值

+ 行插值：按顺序寻找每一行中的空洞像素，设置其像素值与同一行中前一个像素的像素值相同

缩放：将图像乘以一定系数，从而产生新图像的过程

$$
\left\{
\begin{array}{l}
x'=cx\\y'=dy
\end{array}
\right.
$$

$$
\begin{bmatrix}
x'\\y'\\1
\end{bmatrix}=
\begin{bmatrix}
c&0&0\\0&d&0\\0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

+ 沿$x$轴方向缩放$c$倍（$c>1$放大，$0<c<1$缩小），沿$y$轴方向缩放$d$倍（$d>1$放大，$0<d<1$缩小）
+ $c=d$等比缩放，否则为非等比缩放，导致图像变形
+ 缩小——按一定间隔选取某些行和列的像素构成缩小后的新图像；放大——新图像出现空行和空列，可采用插值的方法加以填补，但存在“马赛克”现象

错切：图像的错切变换实际上是景物在平面上的非垂直投影效果

沿$x$轴：

$$
\left\{
\begin{array}{l}
a(x,y)=x+d_xy\\
b(x,y)=y
\end{array}
\right.
$$

沿$y$轴：

$$
\left\{
\begin{array}{l}
a(x,y)=x\\
b(x,y)=y+d_yx
\end{array}
\right.
$$

组合变换：各项简单几何变换的混合操作

$$
\begin{bmatrix}
x'\\y'\\1
\end{bmatrix}=
\begin{bmatrix}
a&b&c\\d&e&f\\g&h&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

>变换矩阵是由构成组合变换的各种简单变换的变换矩阵按从左至右的顺序逐次相乘以后得到的结果
>
>变换矩阵相乘时的顺序是不可以任意改变的
