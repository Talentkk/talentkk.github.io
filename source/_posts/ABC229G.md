---
title: ABC229G
date: 2021/11/28 
description: 　
---

给定一个长度为 $n$ 只含字符 `Y` 和 `.` 的字符串。你可以进行最多 $k$ 次交换两个相邻的字符的操作，问交换完后，可能最长的由 `Y` 组成的连续段有多长。

$1\leq n\leq 2\times 10^5,1\leq k\leq 10^{12}$

考虑初始字符串和最终字符串，`Y` 的相对顺序肯定不变，所以不会有一次操作交换两个 `Y` 。假设第 $i$ 个 `Y` 的位置是 $p_i$ ，如果我们写出一个长度为 `Y` 的个数的序列 $b$ ，其中 $b_i=p_i-i$ 。那么问题就转化为，要对 $b$ 序列进行最多 $k$ 次给某个数 `+1` 或 `-1` 的操作，使得最终 $b$ 序列中某个数 $x$ 的出现的数量尽可能大。因为 $b$ 序列一直是不降的，所以 $b_i=x$ 的位置一定是某个连续段。对于一个连续段 $[l,r]$ 如果要把其中的数都变成一个数，那么这样的代价是:
$$
\sum_{i=l}^{r}{|b_i-x|}
$$
 根据初一课本知识，当 $x$ 取 $b_l,b_{l+1},...,b_r$ 的中位数时代价最小。然后直接 `two pointer` 扫一遍即可。时间复杂度 $O(n)$ 。