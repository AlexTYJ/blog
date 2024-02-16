概念：

+ 状态：状态s包括当前的游戏局面和当前行动的智能体。初始状态so包括初始游戏局面和初始行动的玩家。由于本节讨论的问题假设两个竞争对手轮流行动，因此第i步行动的玩家是确定的，函数player(s)给出状态s下行动的智能体
+ 动作：给定状态s,动作指的是player(s)在当前局面下可以采取的操作a,记动作集合为actions(s)
+ 状态转移：给定状态s和动作a∈actions(s),状态转移函数result(s,a)决定了s在状态采取a动作后所得后继状态
+ 终局状态检测：终止状态检测函数terminal_test(s)用于测试游戏是否在状态s结束
+ 终局得分：终局得分utility(s,p)表示在终局状态s时玩家p的得分。在二人零和博弈中，两名玩家的终局得分之和应该是固定的，因此算法只需记录其中一人的终局得分为utility(s),则另一人的得分可按照零和原则相应算出

决策方法：

$$
\text{minimax}(s)=\left\{\begin{array}{ll}\text{utility}(s),&\text{if terminal_test}(s)\\\max_{a\in\text{action}(s)}\text{minimax}(\text{result}(s,a)),&\text{if player}(s)=\text{MAX}\\\min_{a\in\text{action}(s)}\text{minimax}(\text{result}(s,a)),&\text{if player}(s)=\text{MIN}\end{array}\right.
$$

```
MinimaxDecision:(MAX行动)
	a* ← argmax_{a∈actions(s)}MinValue(result(s,a))
```

```
MaxValue:
	if terminal_test(s) then return utility(s)
	v ← -∞
	foreach a∈actions(s) do
		v ← max(v, MinValue(result(s,a)))
	end
```

```
MinValue:
	if terminal_test(s) then return utility(s)
	v ← +∞
	foreach a∈actions(s) do
		v ← min(v, MaxValue(result(s,a)))
	end
```
