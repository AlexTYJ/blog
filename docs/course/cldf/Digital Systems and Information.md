## 数字系统
### 概念
Takes a set of discrete information <u>inputs</u> and discrete internal information <u>(system state)</u> and generates a set of discrete information <u>outputs</u>.
![Pasted image 20230921103452|300](https://s2.loli.net/2023/09/21/BydNFeEoIZRUP4s.png)
### 分类
+ 无状态表示：组合逻辑电路    `Output = Function(Input)`
+ 有状态表示：时序逻辑电路    `State = Function (State, Input) `    `Output = Function (State) / Function (State, Input)`
	+ 同步(Synchronous)：周期更新

		例：计算机

		![Pasted image 20230921104036|350](https://s2.loli.net/2023/09/21/DcSfMHRex3Xnkiy.png)

	+ 异步(Asynchronous)：随时更新

## 嵌入式系统
概念：Computers as integral parts of other products

IO：
	![Pasted image 20230921104338|450](https://s2.loli.net/2023/09/21/3YNh6KQB5d7CnR1.png)

+ A-to-D：模拟$\to$数字

	![Pasted image 20230921104539|350](https://s2.loli.net/2023/09/21/MpF5fGPBWZuLIAH.png)

```mermaid
graph LR;
A([模拟信号])-->B[采样]-->C[量化]-->D([数字信号])
```

> 香农采样定理：采样频率高于实际频率2倍时，可将采样后的信号恢复为原信号

`例` 音频采样频率为48kHZ：人耳能分辨的最高频率为20kHZ，由香农采样定理，采样频率高于40kHZ.

+ D-to-A：数字$\to$模拟
	![Pasted image 20230921105519|350](https://s2.loli.net/2023/09/21/cHNf7KtiFI8yu4v.png)
```mermaid
graph LR;
A([数字信号])-->B[逆量化]-->C[低通滤波]-->D([模拟信号])
```
> 非连续的波形FFT后产生高频信号，需要滤波

## 信号表示

![Pasted image 20230921110101|450](https://s2.loli.net/2023/09/21/3ylgEX2bYBFstde.png)

噪声容限：

![Pasted image 20230921110329|300](https://s2.loli.net/2023/09/21/O7VX4KdLkhWAbtf.png)

> 二进制编码方式具有最高的噪声容限

01信号存储：

| 元件 | 介质           |
| :--- | -------------- |
| CPU  | 电压           |
| Disk | 磁场方向       |
| CD   | 表面坑洞（光） |
| RAM  | 电容           |

数字表示：$(Number)_r=(\sum_{i=0}^{n-1}A_i\cdot r^i)+(\sum_{j=-m}^{-1}A_j\cdot r^j)$

二进制运算：

+ 带进位的单位加法（全加器）：

	![Pasted image 20230921110858|350](https://s2.loli.net/2023/09/21/gGLr71PyxAsK5Vb.png)

	C：进位输出 S：和
+ 多位加法器：

	![Pasted image 20230921111040|350](https://s2.loli.net/2023/09/21/SU28CshzVAPOtwr.png)

+ 带借位的单位减法：

	![Pasted image 20230921111523|350](https://s2.loli.net/2023/09/21/2KFb6vNiLR7fmQV.png)

+ 多位减法器：

	![Pasted image 20230921111417|350](https://s2.loli.net/2023/09/21/XoLmxTzMJOqnUC2.png)

+ 二进制乘法：$0*0=0 | 1*0=0 | 0*1=0 | 1*1=1$
+ 多位二进制乘法：

	![Pasted image 20230921111302|350](https://s2.loli.net/2023/09/21/MdTcRNPzsaF1Yqx.png)

进制转换：

+ 整数部分：除基取余
+ 小数部分：乘基取整

> 原理：将该数按照关于基的幂级数展开

## 编码
### 分类
+ 数值编码：代表具体数字
+ 非数值编码：不代表具体数字 Given n binary digits (called bits), a binary code is a mapping from a set of represented elements to a subset of the $2^n$ binary numbers.
### 编码方式
+ 独热编码：第i位为1表示i，其它位为0
+ 8,4,-2,-1编码：有权编码，具有位权
	+ 性质：0,9 / 1,8 / ... 互为反码
+ 余3编码：将每个数加3得到
	+ 性质：编码后0,1数量相同（0均值）
+ BCD编码：对每一个十进制数位进行编码
	+ 应用：用于人机交互时的数字显示
	+ 计算：BCD调整时，+6 mod 16相当于-10
+ ASCII码：7位二进制码表示，94个可打印字符，34个不可显示字符
	+ 规律：$0\to30_{16}\quad A\to41_{16}\quad a\to61_{16}$
+ 检错码：引入冗余信息进行检错
	+ 奇偶校验码：在编码后加入一个位，使得新的二进制串中1的个数为奇/偶数个（只能检测1位出错，适用于出错概率低的场景）
	+ 格雷码：相邻两个码位间只有一个二进制位不同
		+ 应用：
			1. 旋转编码器（控制旋转角度），当探测器安装歪斜时会产生中间冗余编码
			2. ==表示系统状态==，改变系统状态时不会出现中间结果
+ UNICODE编码：16位二进制数编码