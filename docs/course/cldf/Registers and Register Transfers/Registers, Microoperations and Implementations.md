寄存器设计模型：

+ 存储元件 + 组合电路
+ 拆分基本单元

寄存器存储：

+ 要求：
	+ 可保存多个时钟周期
	+ 使用load enable加载数据
+ 实现：
	+ D触发器：
		+ 问题：无法保存数据，触发时Q = D
		+ 解决：
			+ 阻塞时钟：仅$\overline{\text{Load}}=0$时可接受上边沿![image.png](https://s2.loli.net/2023/12/07/P3eciCb97S5wDgf.png)
				+ 问题：会造成时钟歪斜
			+ 输出控制返回：选择器 + Q$\leftarrow$D![image.png](https://s2.loli.net/2023/12/07/ZenNPFBpWub3864.png)
			+ 使用SR / JK触发器，具有保持功能

寄存器传输操作：The movement and processing of data stored in registers

+ set of registers
+ operations
+ control of operations
+ microoperations：load, count, shift, add, bitwise OR...

寄存器符号：

+ 表示：字母 + 数字 R2, PC, IR
+ 括号：比特位 R1(1), PC(7:0), PC(L)（高低位）
+ 箭头：数据传输
+ 逗号
+ 方括号：寻址 `*`

条件传输：

+ 例：`if (K1 = 1) then (R2 ← R1)` 
	+ 表示：`K1: (R2 ← R1)`
	+ 图示：
		![image.png|250](https://s2.loli.net/2023/12/07/tTBvlWPbmZA6O8q.png)
> 数据始终准备在R2的输入处，当接收到Load信号后，一旦时钟触发，将完成寄存器传输操作

控制表达式：

例：$\overline XK1:R1\leftarrow R1+R2$

微操作：

例：$(K1+K2):R1\leftarrow R1\lor R3$
> 条件中的+表示逻辑或，运算中的+表示加法

![image.png|300](https://s2.loli.net/2023/12/07/yCTrmiu5xdXHN7M.png)
![image.png|300](https://s2.loli.net/2023/12/07/H6yxZVl4PRdTWnE.png)

Verilog语法：

```Verilog
assign =
<=
+
-
&
|
^
~
<<
>>
A[3:0]
{,}
```

> 一个寄存器的值仅能在一个always块中被更新（一个寄存器实现为一个触发器）

寄存器传输结构：

+ 基于多路复用器
+ 基于总线
+ 三态门总线

基于多路复用器：

![image.png|300](https://s2.loli.net/2023/12/07/AaG9py5H4vY2l8f.png)

K1：1    K2$\overline{\text{K1}}$：10
K1+K2$\overline{\text{K1}}$=K1 + K2，使用或门构成Load输入

![image.png|400](https://s2.loli.net/2023/12/07/kNm7fwJuKAcMUtW.png)

Encoder为优先编码器

优化：Encoder为编码器，MUX为译码器，进行归并

寄存器单元设计：

+ 控制信号输入：
	+ 独热编码：Hold, Load, Shift, Add, (0, 0, 0), (1, 0, 0) , (0, 1, 0),  (0, 0, 1)
	+ 编码后信号

例：

![image.png|400](https://s2.loli.net/2023/12/07/HUI8fKuqwarkdVQ.png)

+ Load输入：Load = CX + CY
+ 选择信号：S1 = CX, S2 = CY
+ 待选信号：D0 = A(保持)， D1 = $A\leftarrow B\oplus A$, D2 = $A\leftarrow B\lor A$

门输入成本：3 to 1 MUX（3 x 2 + 3 = 9）+ 异或 8 + 2 = 19

另解：使用时序电路状态机卡诺图方法

![image.png|400](https://s2.loli.net/2023/12/07/Q9EnXwsBqZrmctg.png)

A次态由1现态+3输入决定，CX = CY = 1为无关项

![image.png|200](https://s2.loli.net/2023/12/07/HKL3S18YA6hMCBc.png)

$D=CXB+A\oplus (CYB)$

门输入成本：（异或按8计）2 + 8 + 2 + 2 = 14

可相互传输的寄存器架构：

![image.png|250](https://s2.loli.net/2023/12/15/9lQvUPrJxAf7gtc.png)

采用MUX2to1选择数据源

性质：

+ 可并行传输
+ 可相互交换：S1=S0=0, L0=L1=1
	+ 问题：计算机指令不采用变量交换指令
		+ 电路开销大：每个寄存器需要MUXN-1to1，门电路成本$O(N^2)$
> 现代计算机并未选用该架构

低电路成本的寄存器交换结构：

![image.png|250](https://s2.loli.net/2023/12/15/8AcVqwvPyanhzMJ.png)

公用总线，寄存器将数据放置在总线上

总线决定目标寄存器的接收数据

+ 缺陷：无法直接交换两个变量

基于三态门的寄存器传输：

![image.png|150](https://s2.loli.net/2023/12/15/896XPBuDZU74JkH.png)

仅使能一个三态门，将输出接在一起

+ 无法实现多寄存器交换
+ 可封装为n引脚输出模块（inout）
	+ 应用：板级芯片连接

移位寄存器：

![image.png|300](https://s2.loli.net/2023/12/15/boKH79XUhO4gZnN.png)

+ 串行输入，并行输出
+ 问题：无法停止传输

并行加载移位寄存器：在触发器前加MUX2to1

![image.png|250](https://s2.loli.net/2023/12/15/v8xHpuf61SjeoyT.png)

+ SHIFT = 1：可移动
+ SHIFT = 0：可设初值

可保持的并行加载移位寄存器：

![image.png|300](https://s2.loli.net/2023/12/15/zYSHoXTkPZsWmEC.png)

换为MUX3to1，将引脚接回去实现保持

可双向移位寄存器：

![image.png|250](https://s2.loli.net/2023/12/15/vAitMCxXuNTn61z.png)

增加为MUX4to1，接入左右信号

统型移位寄存器：可支持任意位数直接移动

分层控制：每一层控制直接移动$2^n$位，控制每一层
