设计流程：

1. Specification：
2. Formulation：
	+ 核心：状态抽象
	+ 得到状态图
3. State Assignment：$n\geqslant\lceil\log_2m\rceil$

例：序列识别器

+ 应用：USB串行通信协议中开始结束序列的识别
+ 描述：识别序列1101
+ 状态：
	+ 初态A：未识别到任何状态
	+ 状态B：识别到1个1
	+ 状态C：识别到2个1
	+ 状态D：识别到110

~~~mermaid
graph LR;
A((A))--"1/0"-->B((B))
B--"1/0"-->C((C))
C--"0/0"-->D((D))
D--"1/1"-->B
A--"0/0"-->A
B--"0/0"-->A
C--"1/0"-->C
D--"0/0"-->A
~~~

改为Moore模型：增加成功识别的状态E

~~~mermaid
graph LR;
A((A/0))--1-->B((B/0))
B--1-->C((C/0))
C--0-->D((D/0))
D--0-->E((E/1))
A--0-->A
B--0-->A
C--1-->C
D--0-->A
E--0-->A
~~~
> B, E不能等效：输出不同

