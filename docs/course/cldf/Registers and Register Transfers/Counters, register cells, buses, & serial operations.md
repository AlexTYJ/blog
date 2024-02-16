## 计数器
概念：Counters are sequential circuits which "count" through a specific state sequence.

功能：count up, count down, or count through other fixed sequences

实现：

+ 纹波计数器

![image.png|250](https://s2.loli.net/2023/12/14/O7WvkIyFX4DPZiV.png)

D = $\overline{\text Q}$：得到低频时钟（分频器）

![image.png|250](https://s2.loli.net/2023/12/14/G8S2igw3MjmNVAf.png)

$T_A=2T_{CP}$

问题：时钟并不是同一个器件提供，时钟歪斜

应用：减少触发次数，降低电路功耗（用于实时时钟电路）

+ 同步计数器：寄存器 + 自增器

![image.png|250](https://s2.loli.net/2023/12/14/zx36pqufGCSnEjT.png)

自增器设计：

+ 性质：高位变换 $\iff$ 低位全为1

使用与门信号链对所有输出信号求与，用低位与结果与自身输出做异或实现切换；第一个与门接计数使能，使能为0时停止计数

![image.png|300](https://s2.loli.net/2023/12/14/uP8zM7fclJm61so.png)

问题：传输延迟

解决：Look Head，换大与门全部接入

![image.png|250](https://s2.loli.net/2023/12/14/oF6Hyn9SAbvP3Ei.png)

推广：

+ 可并行输入设初值的计数器：触发器前加一层MUX2to1，选择保持触发器的值或外部输入

	![image.png|250](https://s2.loli.net/2023/12/14/17zG4ZnXlxhNogk.png)
	
+ 级联计数器：低位计数器计数输出接高位计数器使能（低位计数器向上进位，允许高位计数器向上计数一次）
+ 模N计数器：
	+ 时序电路设计：利用状态表进行设计
	+ 二进制计数器改造：
		+ 清零：
			+ 异步清零：利用触发器R输入
			+ 同步清零：将MUX2to1输入接rst信号
		+ 模N：
			+ 计数至N后直接清零（异步）：

				![image.png|250](https://s2.loli.net/2023/12/14/duibRH86KOfeIxN.png)

				问题：7信号也会出现，出现后立即被杀死，但7的出现可能会导致后续电路被杀死
			+ 计数至N-1后rst置1（同步）：

				![image.png|250](https://s2.loli.net/2023/12/14/n4Vj2DoRql5TAtJ.png)

		+ 改变计数范围：

			![image.png|250](https://s2.loli.net/2023/12/14/OqPSv2YJdkyGRpl.png)

			禁止使用原先的CLEAR为0，将rst导入LOAD处，并行读入初值
			计数上界为$2^n-1$时可直接接CO

## 串行传输
并行读入，串行计算，多模块同步计算

![image.png|250](https://s2.loli.net/2023/12/14/qIuBvASmc74zRGX.png)

