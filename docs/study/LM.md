# 什么是语言模型

language model is a model that estimates the probability of a token or sequence of tokens occurring in a longer sequence of tokens (from https://developers.google.com/)

也即为了一段文本序列 $w_1,w_2,...,w_N$ 计算概率 $P(w_1,w_2,...,w_N)$

由链式法则， $P(w_1,w_2,...,w_N)=P(w_1)P(w_2|w_1)P(w_3|w_1,w_2)...P(w_N|w_1,w_2,...,w_N-1)$

