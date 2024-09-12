# 什么是语言模型

language model is a model that estimates the probability of a token or sequence of tokens occurring in a longer sequence of tokens (from https://developers.google.com/)

也即为了一段文本序列 $w_1,w_2,...,w_N$ 计算概率 $P(w_1,w_2,...,w_N)$

由链式法则， $P(w_1,w_2,...,w_N)=P(w_1)P(w_2|w_1)P(w_3|w_1,w_2)...P(w_N|w_1,w_2,...,w_N-1)$

使用n-gram模型，可以简化该公式 $P(w_i|w_1,w_2,...,w_i-1)=P(w_i|w_{i-n+1},w_{i-n+2},...,2_{i-1})$

ppl:

$$
ppl=e^{-\frac{1}{N}\sum_{i=1}^{N}logP(w_i|w_1,...,w_{i-1})}
$$
