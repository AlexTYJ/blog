## Functions and Functional Blocks
概念：Corresponding to each of the functions is a combinational circuit implementation called a functional block

> 类似于函数，模块重用
> 实例化模块产生相应的物理对应，同步运行

表示：VCC - 1    GND - 0

总线：
![image.png|500](https://s2.loli.net/2023/10/19/MvsYhTZK3kaHwc1.png)

使能逻辑：EN = 0 输出高阻态 EN = 1 正常工作
![image.png|500](https://s2.loli.net/2023/10/19/MKNxI8k4L9gGHzv.png)

译码：n bit$\to$m bit     $n\leqslant m\leqslant 2^n$

+ 作用：进制转换
+ 例：38译码器（默认ABC字母顺序 A作高位）
	![image.png|300](https://s2.loli.net/2023/10/19/RS8Bw4MnkjFNhHU.png)![image.png|300](https://s2.loli.net/2023/10/19/rqtIs1Wvie49gUX.png)
+ 性质：每一位输出对应相应的最小项
	+ 推论：
		1. $n$输入$2^n$输出译码器，输出端接$n$输入与门
		2. 该门的成本 G = $n2^n$
+ 问题：$n$较大时实现成本高
+ 解决：行列译码器
	+ 高位：列    低位：行
	+ 两个n/2译码器输出两两组合构成$(2^{n/2})^2=2^n$，即n译码器
	+ 例：38译码器 = 12译码器 + 42译码器
	+ 成本计算：各译码器成本 + 组合成本（$2^n$个2输入与门）$\dfrac{n}{2}2^{n/2}+2^n*2 <\!\!< n2^n$
	+ 弊端：电路层次变多，性能降低

使能译码器：

| EN  | $A_1$ | $A_0$ | $D_0$ | $D_1$ | $D_2$ | $D_3$ |
| --- | ----- | ----- | ----- | ----- | ----- | ----- |
| 0   | X     | X     | 0     | 0     | 0     | 0     |
| 1   | 0     | 0     | 1     | 0     | 0     | 0     |
| 1   | 0     | 1     | 0     | 1     | 0     | 0     |
| 1   | 1     | 0     | 0     | 0     | 1     | 0     |
| 1   | 1     | 1     | 0     | 0     | 0     | 1     |

+ 实现：在输出端添加使能逻辑（即与EN作与）
> 另一种理解（分配器）：理解为==分配==电路，即A1 A0对D(3:0)进行使能，将EN的信号送至对应输出

+ 应用：实现任意逻辑函数：译码器 + 或门，即化为最小项的或
+ 例：全加器
	![image.png|500](https://s2.loli.net/2023/10/19/9coEZmMznBqRpye.png)

7段数码管显示译码器：

![image.png](https://s2.loli.net/2023/10/26/EdjKtGazSRIXO5Q.png)

+ 电路实现：共阴 / 共阳
![image.png](https://s2.loli.net/2023/10/26/EQNJWSrysenUo13.png)
+ 真值表：
	![image.png|400](https://s2.loli.net/2023/10/26/R8DSxQrwhGJIcO7.png)

编码：编码逆过程 m bit$\to$n bit     $n\leqslant m\leqslant 2^n$

+ 操作：真值表过大；采用逻辑函数的方法
+ 应用：中断系统
	+ 每个事件对应一根信号线，当中断发生时，通过编码告诉处理器哪个中断发生
+ 简单编码器：
	+ $A_3=D_8+D_9$  $A_2=D_4+D_5+D_6+D_7$  $A_1=D_2+D_3+D_6+D_7$  $A_0=D_1+D_3+D_5+D_7+D_9$
	+ 问题：输入信号同时发生时，无法得到合法编码
	+ 解决：优先编码器
+ 优先编码器：输入信号同时发生时，按照优先级选择输出编码
	+ 真值表：D4具有最高优先级
	 ![image.png|400](https://s2.loli.net/2023/10/26/3TUtbiqN25MZEHO.png)

选择器：

+ 组成：
	+ 一系列输入
	+ 一个输出
	+ 一系列选择控制器
+ 多路复用器：
	![image.png|300](https://s2.loli.net/2023/10/26/9rCks3KmtU2QTRM.png)
+ 原理：译码器输出作使能信号，并对输出取或
	![image.png|400](https://s2.loli.net/2023/10/26/2bAe53F4O8iMwqu.png)
+ 多位宽：同位放在一起选择
	![image.png|450](https://s2.loli.net/2023/10/26/sQpevOtgkFAU8fC.png)
+ 三态门实现：三态门输出可短接，省去多输入或门
	![image.png|300](https://s2.loli.net/2023/10/26/rKHIfu7dNjmhWVQ.png)
+ 分层选择：选择低位到高位的奇偶性
	![image.png|350](https://s2.loli.net/2023/10/26/5Gxo3e6LqrmivIs.png)
+ 应用：实现任意逻辑函数
	+ 思路：将输出理解为表(LUT, Look Up Table)，根据输入，利用选择器进行查表
		+ 实现：LUT = MUX + 存储空间
		+ 例：Gray $\to$ Bin
			![image.png|350](https://s2.loli.net/2023/10/26/B6TKuegkjNUb8Yv.png)
	+ 改进：对输入信号进行复用（0, 1, $x,\ \bar x$），从而减少多路复用器的输入规模
		+ 例：
			![image.png](https://s2.loli.net/2023/10/26/ZmfaIHDEJb39Kjn.png)
			![image.png](https://s2.loli.net/2023/10/26/yVBwRtKS7HNCOZj.png)
		+ 缺陷：无法使用LUT方法