色彩：光与物体之间发生反射、折射、散射、传播、吸收以及衍射等产生
 （基本问题：Dichromatic Reflection Separation）

 + 分类：
	 + 彩色 (chromatic color)：红、黄、蓝等单色以及它们的混合色（对光谱各波长的反射具有选择性，在白光照射下呈不同颜色）
	 + 消色 (achromatic color)：灰度，即白色，黑色以及各种深浅不同的灰色（对光谱各波长的反射不具选择性）
+ 色觉：不同波长的光线作用于视网膜而在大脑中引起的感觉
	+ 可见光波长：390 ~ 780 nm
	+ 原理：视网膜视觉细胞
		+ 杆状体：对光极为灵敏，但没有区分色彩的能力（上亿个）
		+ 锥状体：在较强的照度下才能激发，能辨别不同颜色（六、七百万个）
	+ 解释：三原色——视网膜上存在三种对红、绿、蓝光波长特别敏感的视锥细胞或相应的感光色素，当不同波长的光线进入人眼时，与之相符或相近的视锥细胞发生不同程度的兴奋，从而产生视觉（三种视锥细胞受到同等程度的刺激时产生消色）
		+ 标准颜色：R：700nm    G：541.6nm    B：435.8nm
	+ 问题：vision illusion，人眼通过上下文（相对）来判断颜色，绝对色彩不准确
	+ 性质：韦伯定律 $K=\dfrac{\Delta I}{I}$ 刺激差别阈值与刺激强度成正比
	+ 感知的优先程度和灵敏度：
		+ 优先程度：色调（hue, H） > 饱和度（saturation, S） > 亮度（lightness value, V）
		![image.png|250](https://s2.loli.net/2023/10/07/rZybEltGd8wPNIJ.png)
		+ 敏感度：对亮度变化最敏感

> 显示器无法显示人眼可见范围的全部色彩

颜色空间：

+ 颜色空间模型：
	+ 分类：
		+ 设备依赖：RGB, CMY, HSV
		+ 设备无关：CIE XYZ, CIE L\*a\*b, CIE YUV (CIE, Commission Internationale de L‘Eclairage，国际照明委员会)
	+ RGB：三维直角坐标颜色系统中的单位立方体

		![image.png|150](https://s2.loli.net/2023/10/07/oOa79mgwAS5NJ46.png)

		+ 主对角线上各原色的量相等，产生由暗到亮的白色（灰度）
		+ （0，0，0）为黑，（1，1，1）为白，正方体的其他6个角点分别为红、黄、绿、青、蓝和品红
		+ RGB $\subset$ CIE
	+ CMY：Complementary color of RBG —— Cyan, Magenta, Yellow
		+ 相减色，减掉了为视觉系统识别颜色所需要的反射光
		+ 彩色印刷或者彩色打印的纸张不能发射光线，因而印刷机或打印机就只能使用一些能够吸收特定光波而反射其他光波的油墨或者颜色（反射C=G+B意味着吸收R）
	+ RGB VS CMY：

		![image.png|250](https://s2.loli.net/2023/10/07/rV2gFUeidhKSWBA.png)

		+ R+G=Y，R+B=M，G+B=C，R+G+B=W
		+ Y+M=R，C+Y=G，C+M=B，C+M+Y=K
	+ HSV：色调（Hue）、色饱和度（Saturation）和亮度（Intensity / Value），从人的视觉系统出发

		![image.png|150](https://s2.loli.net/2023/10/07/wWHmsgyaNvUj3I9.png)

		+ 圆锥的顶面对应于V=1，包含RGB模型中的R=1，G=1，B=1三个面
		+ H由绕V轴的旋转角给定。红色对应于角度0$^\circ$，绿色对应于角度120$^\circ$，蓝色对应于角度240$^\circ$
		+ 圆锥的顶点处，V=0，H和S无定义，为黑色
		+ 优势：三个坐标独立，彩色之间感觉上的距离与HSV颜色模型坐标上点的欧几里德距离成正比
	+ CIE：独立于设备的颜色
		+ CIE XYZ：由标准观察者配色函数计算得来，以色视觉三元理论为根据

			![image.png](https://s2.loli.net/2023/10/07/m5aLkxiIcFGeYnT.png)

			+ Y为亮度，x,y是从三刺激值XYZ计算得来的色坐标
		+ CIE L\*a\*b：CIE XYZ颜色模型的改进型，以便克服原来的Yxy颜色空间存在的在x，y色度图上相等的距离并不相当于觉察到相等色差的问题

			![image.png](https://s2.loli.net/2023/10/07/iy5NsZk6W9Jnb8Y.png)

			+ L（明亮度），a（绿色到红色）和b（蓝色到黄色）
			+ 颜色的亮度（L）、灰阶和饱和度（a,b）可以单独修正，整个颜色都可以在不改变图像或其亮度的情况下，发生改变
		+ CIE YUV：亮度信号Y和色度信号U、V分离
			+ Used in TV.
	+ 颜色空间的转换：
+ RGB $\leftrightarrow$ CIE：

$$
\begin{bmatrix}
Y\\ U\\ V
\end{bmatrix}=
\begin{bmatrix}
0.299&0.587&0.114\\
-0.147&-0.289&0.435\\
0.615&-0.515&-0.100
\end{bmatrix}
\begin{bmatrix}
R\\ G\\ B
\end{bmatrix}
$$

+ RGB $\leftrightarrow$ CMY：C = 255 - R, M = 255 - G, Y = 255 - B
+ RGB $\leftrightarrow$ HSV：

	![image.png|300](https://s2.loli.net/2023/10/12/Ko6I3qlNMrvhn4T.png)

	![image.png](https://s2.loli.net/2023/10/12/Wiec76tfSDnZdjF.png)


+ RGB $\leftrightarrow$ CIE：

$$
\begin{bmatrix}
X\\ Y\\ Z
\end{bmatrix}=
\begin{bmatrix}
0.608&0.714&0.200\\
0.299&0.587&0.144\\
0.000&0.066&1.112
\end{bmatrix}
\begin{bmatrix}
R\\ G\\ B
\end{bmatrix}
$$

+ CIE XYZ $\leftrightarrow$ CIE L\*a\*b

	![image.png](https://s2.loli.net/2023/10/12/7ve1WMEF4AXOVbD.png)
