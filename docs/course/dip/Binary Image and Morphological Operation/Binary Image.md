概念：Pixel value is limited to 0 or 1.
> For convenience in programming, we usually use 0 OR 255 instead of 0 OR 1 to represent the binary image.

优势：

+ 更小的内存需求 
+ 运行速度更快
+ 为二值图像开发的算法往往可以用于灰度级图像 
+ 更便宜

缺势：

+ 应用范围毕竟有限
+ 更无法推广到三维空间中
+ 表现力欠缺，不能表现物体内部细节
+ 无法控制对比度

构建：阈值化 Thresholding

$$
\left\{
\begin{array}{ll}
I(x,y)=0&if\ I(x,y)<Threshold\\
I(x,y)=255&if\ I(x,y)\geqslant Threshold
\end{array}
\right.
$$

> 阈值设置十分重要

阈值寻找：大津算法

+ 思路：最小化前景/背景内部方差，最大化前景、背景间的方差
$$
\sigma_{within}^2(T)=\dfrac{N_{Fgrd}(T)}{N}\sigma_{Fgrd}^2(T)+\dfrac{N_{Bgrd}(T)}{N}\sigma_{Bgrd}^2(T)
$$
推导：类间方差 = 总方差 - 类内方差 （故最小化类内方差等价于最大化类间方差）

$$
\begin{array}{l}
\sigma_{between}^2(T)=\sigma^2-\sigma_{within}^2(T)\\
=\left(\dfrac{1}{N}\sum_{x,y}(f^2[x,y]-\mu^2)\right)-\dfrac{N_{Fgrd}}{N}\left(\dfrac{1}{N_{Fgrd}}\sum_{x,y\in Fgrd}(f^2[x,y]-\mu_{Fgrd}^2)\right)-\dfrac{N_{Bgrd}}{N}\left(\dfrac{1}{N_{Bgrd}}\sum_{x,y\in Bgrd}(f^2[x,y]-\mu_{Bgrd}^2)\right)\\
=-\mu^2+\dfrac{N_{Fgrd}}{N}\mu^2_{Fgrd}+\dfrac{N_{Bgrd}}{N}\mu^2_{Bgrd}\\
=\dfrac{N_{Fgrd}}{N}(\mu_{Fgrd}-\mu)^2+\dfrac{N_{Bgrd}}{N}(\mu_{Bgrd}-\mu)^2\\
=\dfrac{N_{Fgrd}(T)\cdot N_{Bgrd}(T)}{N^2}\left(\mu_{Fgrd}(T)-\mu_{Bgrd}(T)\right)^2
\end{array}
$$

简化版推导：（直接利用上式方差相关结果）

令$w_f=\dfrac{N_{Fgrd}}{N},w_b=\dfrac{N_{Bgrd}}{N}$，$w_f+w_b=1$
$\mu=w_f\cdot\mu_{Fgrd}+w_b\cdot\mu_{Bgrd}$
$\sigma^2_{between}=w_bw_f(\mu_f-\mu_b)^2$ 

相当于化去全局均值$\mu$，简化计算

+ 步骤：
	1. 确定原始图像中像素的最大值和最小值
	2. 最小值加1作为threshold对原始图像进行二值化操作
	3. 根据对应关系确定前景和背景，分别计算当前threshold下的内部协方差和外部协方差
	4. 回到Step 2直到达到像素最大值
	5. 找到最大外部和最小内部协方差对应的threshold

改进：局部二值化

+ 设定一个局部窗口，在整个图像上滑动该窗口
+ 对于每一窗口位置，确定针对该窗口的threshold

问题：连续线条提取 / 噪声识别

解决：形态学