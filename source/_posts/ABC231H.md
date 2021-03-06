---
title: ABC231H
date: 2021/12/14
description: 　
---

$n$ 行 $m$ 列的网格图中有 $k$ 个棋子 $(a_i,b_i)$ 。一开始所有棋子都是白的，染黑第 $i$ 个棋子的代价是 $c_i$ 。问最少花多少代价，使得每行每列都至少有一个棋子被染黑。

$1\leq n,m,k\leq10^3$

考虑将问题转化到二分图上。左部表示行，右部表示边，对于一个棋子，从行向列连权值为 $c_i$ 的边。于是问题就转化为求最小的权值，将所有点覆盖。

这是一个经典问题。设 $\min(i)$ 表示二分图中与点 $i$ 相邻的边中权值最小值。把每条边 $(u,v,c)$ 的权值改写为 $(u,v,c-\min(u)-\min(v))$ 后，计算出当前图的最小带权匹配 $T$ 。则答案为所有点的 $\min(u)$ 之和加上 $T$ 。

这样做的意义是，先满足每个点都被覆盖，即给每个点都选择和它相邻的最小边，然后再通过选取其它的边进行调整。

时间复杂度 $O(n^2)$ 。  