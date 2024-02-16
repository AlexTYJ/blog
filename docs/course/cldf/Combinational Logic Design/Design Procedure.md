## Combinational Circuits
基本结构：

+ A set of m Boolean inputs
+ A set of n Boolean outputs
+ n switching functions, each mapping the 2m input combinations to an output such that the current output depends only on the current input values
![image.png|400](https://s2.loli.net/2023/10/19/c8WGsFQLPnUj9gT.png)

设计思路：模块拆解（自顶上下） 设计预定义复用模块（IP核）

设计过程：

1. Specification 调研：Write a specification for the circuit if one is not already available
2. Formulation：Derive a truth table or initial Boolean equations that define the required relationships between the inputs and outputs, if not in the specification
3. Optimization：Apply 2-level and multiple-level optimization
4. Technology Mapping：Map the logic diagram or netlist to the implementation technology selected（门 -> 与非 / 或非）
5. Verification：Verify the correctness of the final design manually or using simulation

单元库：

+ 原理图
+ 占用面积
+ 输入负载
+ 传输延迟
+ 映射模板

![image.png](https://s2.loli.net/2023/10/26/nyCkOzxM157JXVY.png)

工艺映射：

+ 假设：忽略门负载、门延迟；目标门与非门均可用
+ NAND映射算法：
	+ AND：后加非    OR：前加非（$A+B=\overline{\overline{AB}}=\overline{\overline A+\overline B}$）
	![image.png|300](https://s2.loli.net/2023/10/26/IrRJyPWFetj8Ezw.png)
	+ 非门推过扇出点，两非门相互抵消
	 ![image.png|500](https://s2.loli.net/2023/10/26/Z8KyQdpnrRW1kO2.png)
	+ 例：
	 ![image.png|450](https://s2.loli.net/2023/10/26/JA4wG9rHD8oiWBC.png)
+ NOR映射算法：AND：前加非    OR：后加非

验证：

+ 真值表
+ 布尔方程
+ HDL仿真
	+ 设计TestCase


