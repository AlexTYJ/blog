# 人工智能原理

这是中国科学院大学人工智能专业本科生课程《人工智能原理》的笔记。

## 1 绪论

---

什么是人工智能？

- 像人一样思考
    - 认知建模：如果我们说某个程序能像人一样思考，那么我们必须有某种办法来确定人是如何思考的
    - 三种方法：
        - 通过内省——试图捕获我们自身的思维过程
        - 通过心理实验——观察一个人的行为
        - 通过脑成像——观察大脑的活动
- 合理地思考
    - “正确思考”：不可反驳的推理过程
    - 困难：
        - 获取非形式的知识并用逻辑表示法要求的形式术语来陈述之时是不容易的，特别是在只是不是百分之百肯定时
        - 消耗大量计算资源
- 像人一样行动
    - 图灵测试：如果一位人类询问者在提出一些书面问题以后不能区分书面回答来自人还是来自计算机，那么这台计算机就通过测试
    - 完全图灵测试：还包括感知物体（计算机视觉）、操纵和移动对象（机器人学）
    - 科学家并未致力于通过图灵测试
- 合理地行动
    - 智能体：某种能够采取行动的东西
    - 理性智能体（Agent）：为取得最佳结果或在存在不确定性时取得最佳期望结果而采取行动
    - 有限合理性：当没有足够时间来完成所有想要做的计算时仍能恰当地行动

人工智能研究三大学派：
  - 符号主义：是指基于符号运算的人工智能学派，他们认为知识可以用符号来表示，认知可以通过符号运算来实现。例如，专家系统等。
  - 联结主义：是指神经网络学派
  - 行为主义：是指进化主义学派，在行为模拟方面，麻省理工学院的布鲁克教授1991年研制成功了能在未知的动态环境中漫游的有6条腿的机器虫。
  - 三大学派的综合集成

人工智能未来发展三大途径：
  - 信息模型：大数据+大算力+强算法的信息技术方法
  - 生命模型：结构仿脑+功能类脑+性能超脑的类脑途径
  - 自主智能模型：强化学习+物理模型+算力
  
---

## 2 智能 Agent

### 2.1 Agent 和环境

感知：表示任何时刻 Agent 的感知输入

感知序列：该 Agent 所有的所有输入数据的完整历史

Agent 在某时刻的行动选择依赖于那个时刻位置该 Agent 的**整个感知序列**。从数学角度就是一个 Agent 函数，将任意给定的感知序列映射为行动。**理论上**可以列表表示（实际上不太可行）。

Agent 函数：Agent 函数是抽象的数学描述

Agent 程序：Agent 程序则是一个具体实现，它在一些物理系统内部运行。

### 2.2 好的行为：理性的概念

理性 Agent：做事**正确**的 Agent。“正确”依赖于性能度量，所以性能度量的合理性很重要。

渴望：通过**性能度量**（比如油耗、时间等等）来表述，他对环境状态的任何给定序列进行评估。

一般原则：根据实际在环境中希望得到的结果来设计性能度量

理性的判断依赖于以下 4 方面：

- 定义成功标准的性能度量。
- Agent 对环境的先验知识。
- Agent 可以完成的行动。
- Agent 截止到此刻的感知序列。

由此得出理性 Agent 的定义：对每一个可能的感知序列，根据已知的感知序列提供的证据和 Agent 具有的先验知识，理性 Agent 应该选择使其性能度量最大化的行动。

明确理性和全知的区别：

全知：明确地知道它的行动产生的实际结果并且做出相应的动作。全知者在现实中是不可能的。

理性不一定完美。

- 理性：**期望**的性能最大化
- 完美：**实际**的性能最大化（现实中不可能）

学习：理性 Agent 不仅要能够收集信息，还要求能从它所感知的信息中尽可能多的学习。Agent 最初的设定可能反应的是环境的先验知识，随着 Agent 经验的丰富，这些知识会被改变或者增加。

自主性：Agent 依赖于设计人员的先验知识而不是它自身的感知信息，这种情况我们会说该 Agent 缺乏自主性。

理性 Agent 应该是自主的。但实践中，很少要求 Agent 从一开始就完全自主。

### 2.3 环境的性质

任务环境（PEAS 描述）：

- Performance（性能）
- Environment（环境）
- Actuators（执行器）
- Sensors（传感器）

环境的分类维度：

- 完全可观察的与部分可观察的
    - 完全可观察的：Agent 的传感器在每个时间点上都能获取环境的完整状态。
    - 有效完全可观察的：传感器能够检测所有与**行动决策相关**的信息。
    - 部分可观察的：噪音、不精确的传感器、或者传感器丢失了部分状态数据。
    - 无法观察的：Agent 无传感器。
- 单 Agent 和多 Agent
    - 单Agent举例：字谜游戏
    - 多Agent举例：下国际象棋
- 确定的与不确定的
    - 确定的：如果环境的下一个状态完全取决于当前状态和Agent执行的动作
    - 不确定的：环境是部分可观察的
- 片段式的与延续式的
    - 片段式： Agent被分割为一个个原子片段，每个片段Agent感知信息并完成单独行动，下一个片段不依赖于以前的片段中采取的行动
    - 延续性：在延续性环境中，当前的决策会影响到所有未来的决策（下棋、出租车驾驶），短期行动会有长期效果
- 静态的与动态的
    - 动态的：如果环境在Agent计算的时候会变化（出租车自动驾驶），动态的环境会持续要求Agent做决策
    - 静态的：相对容易处理，在决策时不需要观察世界，不需要顾虑时间流逝（填字谜游戏）
    - 半动态的：如果环境本身不随时间变化而变化，但是Agent的性能评价随时间变化（国际象棋比赛，要计时）
- 离散的与连续的
    - 环境的状态、时间的处理方式以及Agent的感知信息和行动，都有离散/连续之分
- 已知的与未知的
    - 指的不是环境本身，而是Agent/设计人员的知识状态，知识是指环境的“物理法则”
    - 已知环境中，所有行动的后果（如果环境是随机的，则是指后果的概率）是给定的
    - 未知环境中，需要学习环境是如何工作的，以便做出好的决策
    - 已知的环境可以是部分可观察的（翻牌游戏，已知所有规则），未知的环境可能是完全可观察的（玩新的视频游戏，不知道按钮作用）

### 2.4 Agent 结构

Agent 程序要在某个具备物理传感器和执行器的计算装置上运行，称为体系结构

$$
Agent=体系结构+程序
$$

选择的程序必须适合体系结构

本书中讨论的 Agent 程序具有同样的框架：输入为从传感器得到的**当前**感知信息，返回的是执行器的行动抉择

4 种基本的 Agent 程序：

- 简单反射 Agent ： 条件-行为规则
- 基于模型的反射 Agent
- 基于目标的 Agent：搜索，规划
- 基于效用的 Agent：使其期望效用最大化

学习 Agent

- 原子表示：世界的每个状态是不可见的——它没有内部结构。
- 要素化表示：将状态表示唯变量或特征的集合，每个变量或特征都可能有值。
- 结构化表示：显示描述对象之间的关系。


从上到下，表达力增强，推理和学习也越来越复杂

---

## 第三章 通过搜索进行问题求解

搜索即是指从问题出发寻找解的过程

搜索是基于目标的Agent、

搜索是原子表示

NP完全性：

- P：多项式问题，能够在$O(n^{k})$的时间内解决的问题
- NP：不确定性多项式问题，指存在某个算法能够在多项式时间内猜测出一个该问题的解并验证这个猜测是否正确

开放问题：NP=P ???

### 3.1 问题求解Agent

目标：世界的一个状态集合————目标被满足的那些状态的集合

Agent的任务：找出现在集合未来的行动，以使它达到一个目标的状态

- 没有地图：
- 有地图：

环境可观察、任务环境离散、环境已知、环境确定

一个问题可以用5个组成部分形式化地描述：

- Agent的初始状态
- 描述Agent的可能行动。给定一个特殊状态s，ACTION(s)返回在状态s下可以执行的行动集合
- 对每个行动的描述（正式名称转移模型）,RESULT(s,a).
- 目标测试，确定给定状态是不是目标状态
- 路径耗散函数：为每条路径赋一个耗散值

问题的形式化：抽象（这是个动词）状态描述、行动等


### 3.2 问题实例

真空吸尘器、八数码

### 3.3 通过搜索求解

记录搜索树的数据结构：

- n.STATE
- n.PARENT
- n.ACTION
- n.PATH-COST

三种常见的队列形式：

- 先进先出
- 后进先出，又称之为栈
- 优先级队列：队列中的元素具有根据函数计算出的优先级，总是具有最高优先级的队列出队

评价一个算法的性能考虑四个方面
- 完备性
- 最优性
- 时间复杂度
- 空间复杂度

一些记号：
- b：分支因子，任何结点的最多后继数
- d：目标结点所在的最浅的深度（从根节点到目标状态的步数）
- m：状态空间中任何路径的最大长度

### 3.4 无信息搜索策略

无信息搜索又称盲目搜索，是指除了问题定义中提供的状态信息外没有任何附加信息。

有信息搜索又称启发式搜索，是指知道一个非目标状态是否比其他状态“更有希望”接近目标的策略。

- 宽度优先搜索：时间复杂度$O(b^{d+1})$，空间复杂度$O(b^{d})$
- 一致代价搜索：每次扩展路径消耗最小的节点。同时，目标检测在节点即将扩展的时候进行（这样可以让节点多次更新）
- 深度优先搜索：时间复杂度$O(b^{m})$，空间复杂度$O(bm)$
    - 深度受限搜索：深度为l的节点被当做没有后继对待。时间复杂度$O(b^{l})$，空间复杂度$O(bl)$
    - 迭代加深的深度优先搜索：不断增大深度限制。时间复杂度$O(b^{d})$，空间复杂度$O(bd)$
- 双向搜索：时间和空间复杂度都是$O(b^{\frac{d}{2}})$，但不能保证最优解。且要求目标状态是明确的状态（八皇后就不能用双向搜索）

### 3.5 有信息（启发式）的搜索策略
h(n)=结点n到目标结点的最小代价路径的代价估计值

- 贪婪最佳优先搜索：试图优先扩展目标最近节点，这样可能可以很快找到解
- A*搜索：缩小总评估代价 f(n)=h(n)+g(n)
- 储存受限的启发式搜索

### 3.6 启发式函数

---

### 4.1 局部搜索算法和最优化问题
- 爬山法
    - 随机爬山法
    - 首选爬山法
    - 随机重启爬山法
- 模拟退火
- 局部束搜索
- 遗传算法

### 4.2

---

## 5 对抗搜索和博弈

### 5.1 博弈

- 双人完备信息博弈（下棋）
- 机遇性博弈，存在不可预测性的博弈，如抛硬币

### 5.2 $\alpha \beta$ 剪枝

必考

---

## 6 约束满足问题
### 6.1 定义约束满足问题
一个约束满足问题（CSP）包含三个成分:

- X：变量集合 $\{X_{1},X_{2},...,X_{n}\}$
- D：值域集合 $\{D_{1},D_{2},...,D_{n}\},X_{i}$的值域$D_{i}$由其可能的取值$\{v_{1},v_{2},...,v_{k}\}$组成。
- C：约束集合 Ci是有序对$<\text{scope,rel}>$，其中scope是约束中的变量组，rel定义了变量取值应满足的关系。

实例：地图着色问题、作业调度问题

### 6.2 约束传播：CSP中的推理
- 变量：图中节点
- 约束：图中的胡

结点相容、弧相容

AC-3算法：

### 6.3 CSP的回溯搜索


## 7 

## 8 一阶逻辑

基本句法元素：

- 常量符号：表示对象

- 谓词符号：表示关系

- 函词：表示函数

- 解释：规范以上元素

项：指代对象的逻辑表达式

- 常量符号是项

- 复合项由函词以及紧随其后的参数、被括号括起来的列表项组成，例如：LeftLeg(John)

- 谓词不可能是项

原子语句：有了指代对象的项以及指代关系的谓词，把它们放在一起可形成陈述事实的原子语句。例如：Married(Father(Richard), Mother(John))

复合语句：由逻辑连词构成的语句。例如：¬Brother(LeftLeg(Richard), John)

量词：

- 全称量词

- 存在量词

- 嵌套量词：采用多个量词可以表示更复杂的语句

德摩根律：

- ¬∃𝑥 𝑃 ≡ ∀𝑥 ¬𝑃 

- ¬∀𝑥 𝑃 ≡ ∃𝑥 ¬𝑃 

- ∀𝑥 𝑃 ≡ ¬∃𝑥 ¬𝑃 

- ∃𝑥 𝑃 ≡ ¬∀𝑥 ¬𝑃 

等词：𝐹𝑎𝑡ℎ𝑒𝑟 𝐽𝑜ℎ𝑛 = 𝐻𝑒𝑛𝑟y

语法糖：语法的扩展或缩写


## 9 一阶逻辑的推理

### 命题推理与一阶推理
全称量词实例化：通过用基本项（没有变量的项）置换全称量词来推断任意语句

形式化描述：对于任意语句a、变量v和未在知识库其他地方出现的常量符号k,$\frac{\exists v a}{SUBST({v/k},a)}$

例如：由语句∃𝑥 𝐶𝑟𝑜𝑤𝑛(𝑥) ∧ 𝑂𝑛𝐻𝑒𝑎𝑑(𝑥,𝐽𝑜ℎ𝑛)可以推断出𝐶𝑟𝑜𝑤𝑛(𝐶1) ∧ 𝑂𝑛𝐻𝑒𝑎𝑑(𝐶1,𝐽𝑜ℎ𝑛),只要𝐶1没在知识库的其他地方出现过。在逻辑中，这个新的名称被称为Skolem常数。存在量词的实例化是一种更一般过程的特例，这种一般过程称为Skolem化。

量词的推理规则
- 全称量词实例化可以多次应用从而获得不同的结果
- 存在量词实例化只能应用一次，然后存在量化的语句就可以被抛弃

例如，一旦添加了语句Kill(Murderer, Victim)，就不再需要语句∃x Kill(x, Victim)。严格地说，新知识库逻辑上并不等于旧知识库，但只有在原始知识库可满足时新的知识库才是可满足的，可以证明他们是推理等价的。

### 合一与提升 
置换的结果称为实例。

定义：令$θ=\{v_{1}/t_{1},…v_{n}/t_{n}\}$是一个置换，E是一个表达式，则Eθ是一个同时用项$t_{i}$代替E中变量$v_{i}$所得到的表达式(1≤i≤n)。Eθ称为E的实例。

合一算法UNIFY以两条语句为输入，如果合一置换存在则返回它们的合一置换UNIFY(p,q)=θ，这里SUBST(θ,p) = SUBST(θ,q)。

例子：

- 𝑈𝑁𝐼𝐹𝑌(𝐾𝑛𝑜𝑤𝑠(𝐽𝑜ℎ𝑛, 𝑥),𝐾𝑛𝑜𝑤𝑠(𝑦, 𝑀𝑜𝑡ℎ𝑒𝑟(𝑦)))= {𝑦/𝐽𝑜ℎ𝑛, 𝑥/𝑀𝑜𝑡ℎ𝑒𝑟(𝐽𝑜ℎ𝑛)}
- 𝑈𝑁𝐼𝐹𝑌(𝐾𝑛𝑜𝑤𝑠(𝐽𝑜ℎ𝑛, 𝑥),𝐾𝑛𝑜𝑤𝑠(𝑥, 𝐸𝑙𝑖𝑧𝑎𝑏𝑒𝑡ℎ))= 𝑓𝑎𝑖𝑙𝑢𝑟e

合一子不一定唯一。例子：E={P(x, y), P(x, f(b))}，$θ_{1}$={x/a, y/f(b)} ,$θ_{2}$={x/b, y/f(b)}

最一般合一子：定义：如果对E的每个合一子θ，都存在一个置换λ，使得θ=γ∘λ，则称合一子γ是集合{E1,…, En}的最一般合一子。

### 前向链接
一阶确定子句：一阶确定子句是文字的析取，其中正好只有一个正文字。

前向链接算法：从已知事实出发，触发所有前提得到满足的规则，然后把这些规则的结论加入到已知事实中。

最少剩余值（MRV）启发式：也称“最受约束变量”或“失败优先”启发式（最可能很快导致失败的变量，从而对搜索树剪枝）

### 反向链接
从目标开始反向推导链接规则，以找到支持证明的已知事实。
### 归结：
CNF：合取范式

前束范式：一个公式，如果量词均在全式的开头，它们的作用域延伸到整个公式的末端，则该公式叫做前束范式

Skolem标准范式：以前束范式中消去全部**存在量词**所得到的公式即为Skolem标准范式

Skolem标准型的一般形式是$∀𝑥_{1}∀𝑥_{2} … ∀𝑥_{𝑛} 𝑀(𝑥_{1}, 𝑥_{2}, … , 𝑥_{𝑛})$
其中，𝑀(𝑥_{1}, 𝑥_{2}, … , 𝑥_{𝑛})是一个合取范式，称为Skolem标准型的母式。

## 10 知识工程
### 本体论工程：
本体论工程：表示抽象概念

概念的通用框架被称为上位本体论，按照画图惯例：一般概念在上面，而更具体的概念在下面

#### 通用本体论与专用本体论

所有专用本体论能收敛到一种通用的本体论吗？经过数个世纪哲学和计算的研究，答案是“有可能”

1. 通用本体论在所有专用领域都应该能或多或少地适用（在增加论域特定的公理后）。这意味着它不能无视任何表示问题

2. 在所有足够复杂的论域中，不同领域的知识必须是统一的，因为推理和问题求解可能会同时涉及数个领域。

### 类别和对象

用一阶逻辑表示类别有两种选择：谓词和对象。

两个或者以上类别，如果它们没有公共的成员，则称它们是不相交(disjoint)的。

不相交的完全分解被称为划分

- Partof:类似子集（但不是集合，是个体）

- Bunchof:Partof的反面，（类似超集？），但是并不是集合，而是个体的总和

- 量度(measure)：赋予高度、质量、成本属性的值

- 物体与物质：物体可分，物质不可分

- 固有与非固有：固有的属性在划分时不变，非固有的改变

情景演算的适用性是有限的：它被设计来描述一个世界，其中的动作是离散的、瞬间的、一次发生一个动作

例如给浴盆装水。情景演算能够说出，在这个动作之前浴盆是空的，动作完成之后浴盆是满的，但它不能说出在动作期间发生了什么

例如，等浴盆装水的时候同时刷牙。为了处理这种情况，我们引入称为事件演算的另一种形式体系，它是基于时间点而不基于情景的

- 流𝐴𝑡(𝑆ℎ𝑎𝑛𝑘𝑎𝑟, 𝐵𝑒𝑟𝑘𝑒𝑙𝑒𝑦)是一个对象，指𝑆ℎ𝑎𝑛𝑘𝑎𝑟在𝐵𝑒𝑟𝑘𝑒𝑙𝑒这个事实，但这个事实是否成立它本身并没有说出任何信息。为了声称一个流实际上在某些时间点成立，我们使用像𝑇(𝐴𝑡(𝑆ℎ𝑎𝑛𝑘𝑎𝑟, 𝐵𝑒𝑟𝑘𝑒𝑙𝑒𝑦),𝑡)中一样的谓词T

- 事件：描述为事件类别的实例。使用𝐻𝑎𝑝𝑝𝑒𝑛𝑠(𝐸1, 𝑖)来表示事件𝐸1发生在时间区间i，用𝐸𝑥𝑡𝑒𝑛𝑡(𝐸1) = 𝑖的函数形式也表示同样的意思。

一个事件演算版本完整的谓词集为：见ppt37页

从对象是一部分时空的角度来看，对象可以被看作一般化的事件。可以用状态流(fluents)来描述。

### 精神对象和模态逻辑
精神对象是指某些人脑子中的知识

- 指代透明性
    - 2+2=4且4＜5，希望智能体知道2+2＜5
- 指代不透明性
    - “believe”，“know”，需要指代不透明性，因为并非所有的智能体都知道哪些项是指代同一个对象的
- 模态逻辑
    - A认识P，记为$K_{A}P$，其中K是知识的模态算子

### 类别的推理系统
- 语义网络为知识库可视化提供图形的帮助，并为在类别隶属关系基础上推断对象的属性提供有效算法

- 描述逻辑为构建和组合类别定义提供形式语言，并为判定类别之间的子集和超集关系提供有效算法

- CLASSIC语言

## 11 经典规划
要素化表示：用一组变量表示世界的一个状态的方法。可使用一种称为PDDL(planning domain definition language)的语言。

PDDL如何定义一个搜索问题：初始状态、在一个状态可用的动作、应用一个动作后的结果以及目标测试

基本的PDDL可以处理经典规划领域。扩展的PDDL可以处理连续的、部分可观测的、并发的和多智能体的非经典领域。

### 定义

#### 初始状态
- 每个状态表示为基本原子流（状态变量的同义词）的合取，这些流是**基元的（无变量的）**、**无函数的原子**

- 在一个状态中，以下的流是不允许的：
𝐴𝑡(𝑥, 𝑦)（因为有变量），¬𝑃𝑜𝑜𝑟（因为它是否定式）以及𝐴𝑡(𝐹𝑎𝑡ℎ𝑒𝑟(𝐹𝑟𝑒𝑑), 𝑆𝑦𝑑𝑛𝑒𝑦)（因为使用了函数符号）

使用数据库语义：封闭世界假设意味着任何没有提到的流都是假的。

精心设计状态的表示，以使状态作为流的合取对待，可用逻辑推理来操作；或作为流的集合对待，可用集合运算来操作。有时，集合语义更容易处理

#### 动作

动作可用隐式定义了问题求解搜索所需要的ACTIONS(s)和RESULT(s,a)的一组动作模式来描述。即作为动作的结果，什么发生变化，什么保持不变。

PDDL根据什么发生了变化来描述一个动作结果；不提及所有保持不变的东西

如果状态s满足前提，称在状态s动作α是适用的


### 状态空间搜索规划算法
- 前向（前进）状态空间搜索

- 后向（后退）相关状态搜索

### 规划图
- 最大层启发式
    - 取任何目标的最大层次代价；
    - 可采纳，但不一定是最准确的层次和启发式
- 遵守子目标独立性假设，返回目标的层次代价之和；
    - 可能是不可采纳的，但在实际中对于可大规模分解的问题效果很好集合层次启发式
    - 找到合取目标中的所有文字出现在规划图中的层次，这一层没有任何一对文字是互斥的
- 可采纳的，比最大层启发式占优势，对于在子规划间的交互处理得很好的任务效果非常好

GRAPHPLAN算法反复地调用EXPAND-GRAPH向规划图增加一层。

## 12 不确定性的量化

决策理论=概率理论+效用理论

朴素贝叶斯 (naïve Bayes)：给定原因时，所有这些结果都是条件独立的。其完全联合分布可以写成：

$ P(Cause,Effect_{1},...,Effect_{n})=P(Cause)$


## 13 概率推理

### 不确定性问题域中的知识表示

CPT：条件概率表



贝叶斯网络是一个有向图，其中每个结点都标注了定量的概率信息。其完整的描述如下：
1. 每个结点对应一个随机变量，这个变量可以是离散的或者连续的

2. 一组有向边或箭头连接结点对。如果有从结点X指向结点Y的箭头，则称X是Y的一个父节点。因为图中没有有向回路，也被称为有向无环图，简写为DAG

3. 每个结点$x_{i}$有一个条件概率分布$𝑃(𝑋_{i}|𝑃𝑎𝑟𝑒𝑛𝑡𝑠(𝑋_{i}))$，量化其父结点对该结点的影响

### 贝叶斯网络的语义

结论：
- 给定父结点，一个结点条件独立于其他祖先结点
- 给定父结点后，每个变量条件独立于它的非后代结点
- 给定一个变量的父结点、子结点和子结点的父结点（马
尔科夫覆盖），其条件独立于网络中所有其他结点

用一个符合某种标准模式的规范分布(canonical distribution)来描述。

## 14 时间上的概率推理
- 


## 15 样例学习
### 监督学习
### 决策树

最重要属性：对于样例分类有最大差异的属性
### 非参数化模型

### 支持向量机




## 考试重点
### 第二章
- 环境的规范化描述：PEAS描述（Performance性能,Environment环境,Actuators执行器,Sensors传感器）

- 环境分类维度：
    - 完全可观察的与部分可观察的
        - 完全可观察的：Agent的传感器在每个时间点上都能获取环境的完整状态
        - 有效完全可观察的：传感器能够检测所有与行动决策相关的信息，相关的程序则取决于性能度量。
        - 部分可观察的：噪音、不精确的传感器、或者传感器丢失了部分状态数据
        - 无法观察的：Agent根本没有传感器
    - 单Agent和多Agent
    - 确定的与随机的
        - 确定的：如果环境的下一个状态完全取决于当前状态和Agent执行的动作，则该环境是确定的
        - 不确定的：环境是部分可观察的
    - 片段式的与延续式的
        - 片段式环境：Agent的经历被分成一个个原子片段，每个片段Agent感知信息并完成单独行动，下一个片段不依赖于以前的片段中采取的行动
        - 在延续性环境中，当前的决策会影响到所有未来的角儿（下棋、出租车驾驶），短期行动会有长期效果
    - 静态的与动态的
        - 动态的：如果环境在Agent计算的时候会变化（出租车自动驾驶），动态的环境会持续要求Agent做决策
        - 静态的：相对容易处理，在决策时不需要观察世界，不需要顾虑时间流逝（填字谜游戏）
        - 半动态的：如果环境本身不随时间变化而变化，但是Agent的性能评价随时间变化（国际象棋比赛，要计时）
    - 离散的与连续的
    - 已知的与未知的：指的不是环境本身，而是Agent/设计人员的知识状态，知识是指环境的“物理法则”
        - 已知环境：所有行动的后果（如果环境是随机的，则是指后果的概率）是给定的
        - 未知环境：需要学习环境是如何工作的，以便做出好的决策
        - 已知的环境可以是部分可观察的（翻牌游戏，已知所有规则），未知的环境可能是完全可观察的（玩新的视频游戏，不知道按钮作用）

- Agent函数与Agent程序
    - Agent函数是抽象的数学描述，是一个映射关系，从数学角度来说，Agent函数描述了Agent的行为， 它将任意给定感知序列映射为行动。
    - Agent程序则是一个具体实现，它在一些物理系统内部运行。
    - 从Agent内部看，人造Agent的Agent函数通过Agent程序实现。

- 4种基本的Agent程序
    - 简单反射Agent：基于当前的感知选择行动，不关注感知历史
    - 基于模型的反射Agent：知道世界如何独立于Agent发展的信息和Agent自身的行动如何影响世界的信息
    - 基于目标的Agent：– 把目标信息和模型相结合（和基于模型的反射Agent用来更新内部状态的信息相同），以选择能达到目标的行动
    - 基于效用的Agent：Agent的效用函数是性能度量的内在化，体现对各世界状态偏好程度


### 第三章

- 一个问题可以用5个组成部分形式化地描述
    - 初始状态
    - 可能行动：给定一个特殊状态s，ACTIONS(s)返回在状态s下可以执行的行动集合
    - 转移模型（对每个行动的描述）：用函数RESULT(s, a)描述，表示在状态s下执行行动a后达到的状态
    - 目标测试：确定给定的状态是不是目标状态
    - 路径耗散函数：为每条路径赋一个耗散值，即边加权。问题求解Agent选择能反映它自己的性能度量的耗散函数。

- 搜索算法
    - 无信息
        - 宽度优先搜索：
            - 完备的
            - 不一定最优、但是一定最浅；如果路径代价是基于节点深度的非递减函数，则为最优的。
            - 时间复杂度$O(b^{d+1})$，深度为d，宽度为b
            - 空间复杂度$O(b^{d})$
        - 一致代价搜索：对任何单步代价函数都是最优的，每次扩展路径消耗g(n)最小的，
            - 完备的
            - 一定最优
            - 时间复杂度:$O(b^{[C^*/s]+1})$,最优解的成本为C*,最低代价为 $s$
            - 空间复杂度:$O(b^{[C^*/s]+1})$
            - 区别于宽搜：
                - 目标检测应用于结点被选择扩展时，而不是在结点生成的时候进行
                - 如果边缘中的结点有更好的路径达到该结点那么会引入一个测试
        - 深度优先搜索：
            - 完备的
            - 不一定最优
            - 时间复杂度 $O(b^{m})$，m指任一结点的最大深度
            - 空间复杂度O(bm)，变种回溯搜索为 O(m)
        - 深度受限搜索：
            - 不完备
            - 不一定最优
            - 空间复杂度：$O(bl)$
            - 时间复杂度：$O(b^l)$
        - 迭代加深的深度优先搜索：
            - 完备
            - 不一定最优
            - 空间复杂度：$O(bd)$
            - 时间复杂度：$O(b^{d})$
        - 双向搜索：
            - 完备
            - 不一定最优
            - 空间复杂度：$O(b^{\frac{d}{2}})$
            - 时间复杂度：$O(b^{\frac{d}{2}})$
    - 有信息（启发式）：
        - 贪婪最佳优先搜索：试图扩展离目标最近结点
            - 完备
            - 不一定最优
            - 空间复杂度：最坏$O(b^{m})$
            - 时间复杂度：最坏$O(b^{m})$
        - A*搜索：缩小总评估代价：f(n)=g(n)+h(n)=经过结点n的最小代价解的估计代价
            - 完备
            - 一定最优
            - 空间复杂度：
            - 时间复杂度：
            - 启发式函数的条件：
                - 可采纳启发式（可容许性）：从不会过高估计到目标的代价，即估计值小于等于实际值（直线距离就可以）
                    - 如果h(n)是可采纳的，那么A*的树搜索版本是最优的
                - 一致性（单调性）：如果对于每一个结点n和通过任一行动a生成的n的每个后继结点n’，从结点n达到目标的估计代价不大于从n到n’的单步代价与从n’到达目标的估计代价之和：h(n)≤c(n,a,n’)+h(n’)
                    - 如果h(n)是一致的，那么图搜索的A*版本是最优的
                - 一致性一定保证了可容许性，但是可容许性不一定保证一致性
            - 有效分支因子b*：对于某一个问题，如果A\*算法生成的总结点数为N，解的深度为d，那么b\*就是深度为d的标准搜索树为了能够包括N+1个结点所必须的分支因子。即：$N+1=1+b*+(b*)^{2}+...+(b*)^{d}$
        - 迭代加深A*算法(IDA\*)：截断值用f代价(g+h)代替搜索深度
            
        - 递归最佳优先搜索（RBFS）：每次选最小的

### 第四章
- 局部束搜索：记录k个状态而不是只记录一个，他从k个随机生成的状态开始，每一步全部k个状态的所有后继状态全部被生成。如果其中有一个是目标状态，则算法停止；否则，它从整个后继列表中选择k个最佳的后继，重复这个过程。

- 随机束搜索算法不是从候选后继集合中选择最好的k个后继状态，而是随机选择k个后继状态，其中选择给定后继状态的概率是状态值的递增函数

### 第五章
- 极大值层的下界成为$\alpha$
- 极小值层的上界称为$\beta$

- $\alpha$剪枝：$\alpha（先辈，极大）>= \beta(后继，极小) $
- $\beta$剪枝： $\alpha（后继，极大）>= \beta(先辈，极小) $

### 第六章
- CSP（Constraint satisfaction problem，约束满足问题）定义：XDC
    - X：变量集合
    - D：值域集合
    - C：约束集合，为有序对<scope,rel>，其中scope是约束中的变量组，rel定义了变量组的关系

- 定义状态空间和解：
    - 问题的状态由对部分或者全部变量的一个赋值来定义
    - 相容的：不违反任何约束条件    
    - 完整赋值：每个变量都已赋值；部分赋值：只有部分变量赋值；
    - CSP的解：相容的、完整的赋值

- 结点相容：若单变量值域中所有取值都满足一元约束，就称这个变量是结点相容的

- 弧相容：若某变量值域中的所有取值满足该变量的所有二元约束，则称此变量是弧相容。
    - 更形式的，对于变量$X_{i},X_{j}$，若对$D_{i}$中每个数值在$D_{j}$中都存在数值满足弧$(X_{i},X_{j})$的二元约束，则称$X_{i}$对于$X_{j}$是弧相容的
    - 如果每个变量相对其他变量都是弧相容的，则称该网络是弧相容的

- AC-3算法：
    - 步骤：
        1. 初始化一个队列包含所有弧
        2. 弹出弧（$X_{i}$，$X_{j}$），检查这个弧，如果$D_{i}$全部满足，就处理下一条弧。如果不能全部满足，就删掉不能满足的取值（把D缩小至可以满足），再将所有指向$X_{i}$的弧插入队列
        3. 如果$D_{i}$是空集，则整个CSP没有相容解；否则继续检查直到队列中没有弧
    - 复杂度：假设CSP中有n个变量，变量值域最大为d个元素，c个二元约束。每条弧最多只能插入队列d次，因为至多有d个值可删除。检验一条弧的相容性可以在O($d^{2}$)时间内完成，最坏情况算法的时间复杂度为O($cd^{3}$)
    - 可能会失败，所以需要更强的相容概念

- 路径相容：两个变量的集合{$X_{i}$, $X_{j}$}对于第三个变量Xm是相容的，指对{$X_{i}$, $X_{j}$}的每一个相容赋值{$X_{i}$=a, $X_{j}$=b}，Xm都有合适的取值同时使得{$X_{i}$, $X_{m}$}和{$X_{m}$, $X_{j}$}是相容的

- k-相容：如果对于任何k-1个变量的相容赋值，第k个变量总能被赋予一个和前k-1个变量相容的值，则此CSP是k相容的
    - 1-相容，2-相容，3-相容分别对应结点、弧、路径相容
    - 强k相容：如果一个图满足任意 j(1≤j≤k)，都是j-相容的

- 全局约束：可能涉及任意个约束变量

- 资源约束（atmost约束）
    - 例如：atmost(10, P1, P2，P3, P4)指执行四项任务的总人数不超过10人

- 问题的结构：
    - 树结构CSP：n个结点的树有n-1条弧，O(n)步内改成直接弧相容（从叶子结点往上），然后从根节点往下赋值即可
    - 约束图转化为树：
        - 基于删除节点
            - 环割集：从CSP的变量中选择子集S，使得约束图在删除S后成为一棵树。S称为环割集。找最小环割集市NP-hard问题，但是有近似算法
            - 时间复杂度$O(d^{c}(n-c)d^{2})$，其中c为环割集大小，最坏情况为n-2
        - 基于合并节点
            - 以约束图的树分解为基础，把约束图分解为相关联的子问题，树分解必须满足以下3个条件：
                1. 原始问题中的每个变量至少在一个子问题中出现
                2. 如果两个变量在原问题中由约束相连，那么它们至少同时出现在一个子问题中（连同他们的约束）
                3. 如果一个变量出现在树中的两个子问题中，那么它必须出现在连接这两个子问题的路径上的所有子问题里
            - 前两个条件保证变量和约束都在分解中有表示，第三个条件反映了任何给定变量在每个子问题中必须取值相同的约束

        - 图的树分解的树宽是最大的子问题的大小减1，图本身的树宽定义为它所有树分解的最小树宽
    - 值对称：打破对称结构可以缩小n!倍
        - 多项式时间内找到约束来消除对称性并保留一个对称是可能的，但消除搜索过程中所有中间值集合的对称性是NP-hard

### 第九章
- 置换的结果称为实例。
- 定义：令$θ=\{v_{1}/t_{1},…v_{n}/t_{n}\}$是一个置换，E是一个表达式，则Eθ是一个同时用项$t_{i}$代替E中变量$v_{i}$所得到的表达式(1≤i≤n)。Eθ称为E的实例。
- 合一算法UNIFY以两条语句为输入，如果合一置换存在则返回它们的合一置换UNIFY(p,q)=θ，这里SUBST(θ,p) = SUBST(θ,q)。
    - 例子：
        - 𝑈𝑁𝐼𝐹𝑌(𝐾𝑛𝑜𝑤𝑠(𝐽𝑜ℎ𝑛, 𝑥),𝐾𝑛𝑜𝑤𝑠(𝑦, 𝑀𝑜𝑡ℎ𝑒𝑟(𝑦)))= {𝑦/𝐽𝑜ℎ𝑛, 𝑥/𝑀𝑜𝑡ℎ𝑒𝑟(𝐽𝑜ℎ𝑛)}
        - 𝑈𝑁𝐼𝐹𝑌(𝐾𝑛𝑜𝑤𝑠(𝐽𝑜ℎ𝑛, 𝑥),𝐾𝑛𝑜𝑤𝑠(𝑥, 𝐸𝑙𝑖𝑧𝑎𝑏𝑒𝑡ℎ))= 𝑓𝑎𝑖𝑙𝑢𝑟e
- 合一子不一定唯一。例子：E={P(x, y), P(x, f(b))}，$θ_{1}$={x/a, y/f(b)} ,$θ_{2}$={x/b, y/f(b)}
- 一阶确定子句：一阶确定子句是文字的析取，其中正好只有一个正文字。
- 最少剩余值（MRV）启发式：也称“最受约束变量”或“失败优先”启发式（最可能很快导致失败的变量，从而对搜索树剪枝）
- 归结：
    - CNF：合取范式
    - 前束范式：一个公式，如果量词均在全式的开头，它们的作用域延伸到整个公式的末端，则该公式叫做前束范式
    - Skolem标准范式：以前束范式中消去全部**存在量词**所得到的公式即为Skolem标准范式
    - Skolem标准型的一般形式是$∀𝑥_{1}∀𝑥_{2} … ∀𝑥_{𝑛} 𝑀(𝑥_{1}, 𝑥_{2}, … , 𝑥_{𝑛})$ 其中，$𝑀(𝑥_{1}, 𝑥_{2}, … , 𝑥_{𝑛})$是一个合取范式，称为Skolem标准型的母式。

### 第十四章
- 五大基本任务：
    - 滤波：给定目前为止的所有证据，计算当前状态的后验概率分布
    - 预测：给定目前为止的所有证据，计算未来状态的后验分布
    - 平滑：给定目前为止的所有证据，计算过去某一个状态的后验概率
    - 最可能解释：给定观察序列，可能希望找到最可能生成这些观察结果的状态序列
    - 学习：推理为哪些转移确实会发生和哪些状态会产生传感器读数提供了估计，而且这些估计可以用于对模型进行更新；更新过的模型又提供新的估计，这个过程迭代至收敛

---


## 作业及个人解答
### 第一章
1.反射行动（比如从热炉子上缩回你的手）是理性的吗？它们是智能的吗？

&emsp;答：是理性的；是智能的。

2.以下的计算机系统在何种程度上是人工智能的实例：
  - 超市条码扫描器
  - 网络搜索引擎
  - 语音激活的电话菜单
  - 对网络状态动态响应的网络路由算法

&emsp;答：条码扫描器可以识别条形码的信息；网络搜索引擎可以通过关键词模糊定位结果；语音激活的电话菜单可以语音识别；对网络状态动态响应的网络路由算法可以实时动态分配带宽。

3.为什么进化会倾向于导致行为合理的系统？设计这样的系统想达到的目标是什么？

&emsp;答：行为不合理的系统容易犯错误导致自身受到损害，无法生存；设计这样的系统想达到的目标是或得一个理性的Agent。

### 第二章
1.对于下列活动，分别给出任务环境的PEAS描述，并按2.3.2节列出的性质进行分析：

- 足球运动
- 探索Titan的地下海洋
- 在互联网上购买AI旧书
- 打一场网球比赛
- 对着墙壁练网球
- 完成一次跳高
- 织一件毛衣
- 在一次拍卖中对一个物品投标

答：

- 足球运动：
    - P: 进球数；E：场地、队友配合；A：腿；S：眼睛、耳朵。
    - 部分可观察的、多Agent、不确定的、延续性的、动态的、（环境的状态、时间的处理方式都是）连续的、未知的。
- 探索Titan的地下海洋：
    - P: 探索成果和能力；E：地下海洋环境及海洋生物；A：发动机、灯、机械臂；S：传感器、摄像头。
    - 部分可观察的、单Agent、不确定的、延续性的、动态的、（环境的状态、时间的处理方式都是）连续的、未知的。
- 在互联网上购买AI旧书：
    - P: 性价比；E：互联网信息；A：购买按钮；S：屏幕。
    - 部分可观察的、多Agent、确定的、延续的、静态的、环境状态离散、时间处理方式离散、感知信息和行动离散、未知的。
- 打一场网球比赛：
    - P：得分；E:对手动作、球拍质量；A：手；S：眼睛、耳朵。
    - 完全可观察的、双Agent、不确定的、片段式的、动态的、（环境的状态、时间的处理方式都是）连续的、未知的。
- 对着墙壁练网球：
    - P：连续球个数；E:反弹球力度、速度、角度；球拍质量；A：手；S：眼睛、耳朵。
    - 完全可观察的、单Agent、不确定的、延续性的、动态的、（环境的状态、时间的处理方式都是）连续的、未知的。
- 完成一次跳高：
    - P：调高高度、是否成功；E：杆子的高度；A：膝盖、手；S：眼睛。
    - 完全可观察的、单Agent、随机的、延续性的、静态的、（环境的状态、时间的处理方式都是）连续的、已知的。
- 织一件毛衣：
    - P：毛衣质量、织毛衣速度；E：毛线种类；A：手；S：眼睛。
    - 完全可观察的、单Agent、确定的、延续性的、静态的、（环境的状态、时间的处理方式都是）连续的、已知的。
- 在一次拍卖中对一个物品投标
    - P：价格、对手竞价情况；E：商品价格估计、对手报价；A：手；S：眼睛、耳朵。
    - 完全可观察的、多Agent、随机的、延续性的、静态的、（环境的状态、时间的处理方式都是）离散的、未知的。
  


## 划重点

1. 绪论了解，不做太多要求

2. 第二章：智能体  P4 描述 感知器啥的  属性：完全可观测……  结构：程序和函数的关系

3. 第三章：搜索 搜索算法 无信息、有信息（启发式，A*搜索**必考**，启发式函数的要求，一致性，可容许性）  树搜索、图搜索

4. 第四章；复杂环境的搜索  爬山、模拟退火…… 全局极大值  局部树搜索 P115 在线、离线算法。这一块不用算、概念了解

5. 第五章：对抗搜索  阿尔法β剪枝**必考**，有机会节点、有机会博弈

6. 第六章：约束-满足问题：一致性：弧一致性等概念要掌握

7. 第七章：逻辑  前向链接等   回溯算法不用考，基本概念要有

8. 第八章：多两个量词

9. 第九章：

10. 知识表示不考，规划不考

11. 概率：和作业形式一样

12. 机器学习：了解


## 习题课

选择题 25%

判断题 15%

简答题 30%（写知识点、想法）

计算题 30%

无编程题

### 第二章

拥有智能的最低标准是理性





