可编程逻辑器件

+ 技术：
	+ Mask programming：工厂排线
	+ Fuse：利用代码控制电流烧结电路
	+ Antifuse
	+ Single-bit storage element：利用比特位控晶体管
	+ Build lookup table (LUT)：
		+ 本质：多路选择器 + 真值表实现任意逻辑函数
	+ Transistor Switching Control：
		+ 浮动三级门：Erasable $\to$ Electrically erasable $\to$ Flash
+ 特性：
	+ Permanent：
		+ Mask programming
		+ Fuse
		+ Antifuse
	+ Reprogrammable：
		+ Volatile：断电易失
		+ Non-Volatile

可编程配置：

+ ROM（只读存储器）：固定与门阵列与可编程或门阵列
+ PAL（可编程阵列逻辑）：可编程与门阵列与固定或门阵列
+ PLA：可编程与门阵列、可编程或门阵列
+ CPLD / FPGA

## ROM
原理：n位译码器（固定与门） + 或门（可变或门） = 任意逻辑函数

结构：

![image.png|250](https://s2.loli.net/2023/12/07/8sce1pjMNzqmECw.png)

交叉点处可选择是否连接

存储器观点：对于不同的输入（地址），调取不同的值

## PAL
优势：可实现更多输入输出的逻辑函数

缺陷：部分逻辑函数无法实现

结构：

![image.png|300](https://s2.loli.net/2023/12/07/N5JqOEf64leSUpB.png)

1. 竖线接变量及其反变量
2. 为了实现多于3个与项的逻辑函数，将第一个输出反馈

## PLA
优势：

+ 可实现多输入输出
+ 与项可被任意连接，克服PAL与或结构的数量限制

缺陷：

+ 与项有限
+ 无反馈，无法是实现PAL中的多级电路

结构：

![image.png|400](https://s2.loli.net/2023/12/07/7wphliB56nWEkYH.png)

可编程与门 + 可编程或门 + 可控求反

可重用与项

与门资源有限，利用求反实现多种逻辑函数与项共用
