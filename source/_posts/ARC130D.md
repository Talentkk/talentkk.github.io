---
title: ARC130D
date: 2021/11/29 
description: 　
---

给一棵 $n$ 个节点的数，求有多少合法的排列长度为 $n$ 的排列 $P$，满足对于任意 $a,b,c$ ，如果 $a,b$ 相邻，$b,c$ 相邻，那么有 $P_a<P_b>P_c$ 或 $P_a>P_b<P_c$ 成立。对 $998244353$ 取模。

$1\leq n\leq 3000$

容易发现，对于一个节点 $u$ ，它要么比周围的节点都大，要么比周围的节点都小。我们把第一种情况的 $u$ 成为大点，第二种称为小点。

那么如果 $1$ 是大点还是小点确定了，所有点是大点还是小点也确定了（类似于黑白染色）。我们又观察到对于一个合法的排列 $P$ ，将 $P_i=n+1-P_i$ 后，对于任意一个点 $u$ ，它是大点就会变成小点，是小点就会变成大点。所以得出结论：**一个点是大点的方案和是小点的方案是一一对应的**。

考虑设 $dp(u,x)$ 表示对 $u$ 的这颗子树分配排列（$[1,siz_u]$），$u$ 分配到 $i$ 且 $u$ 是小点的方案数。现在假设我们已经得到了 $u$ 的所有儿子的 $dp$ 值 。根据上面的结论，如果我们设 $g(u,i)$ 为对 $u$ 的这颗子树分配排列，$u$ 分配到 $i$ 且 $u$ 是大点的方案数，则有$g(u,i)=f(u,siz(u)+1-i)$ ，接下来的过程中，我们是先假设 $u$ 是大点，计算 $g(u,i)$ ，再根据等式得到 $dp(u,i)$ 。

先假设 $u$ 只有两个儿子 $x$ 和 $y$ ，其中 $siz_x=n,siz_y=m$ ，则我们只关心 $x$ 和 $y$ 中 $P$ 值较大的那个。我们设 $f(i)$ 表示对 $x$ 和 $y$ 两棵子树进行分配，且 $\max(P_x,P_y)=i$ 的方案数。比如先假设 $P_x$ 更大，则我们枚举 $x$ 在 $x$ 的子树中是第 $i$ 大的，以及 $y$ 的子树中有 $j$ 个数比 $P_x$ 小，则有转移方程：
$$
f(i+j)\leftarrow dp(x,i)\times\sum_{k=1}^{j}dp(y,k) \times {i+j-1 \choose i-1}\times{n-i+m-j\choose n-i}
$$
预先将 $dp(y,i)$ 前缀和后，这一步的复杂度是 $siz_x\times siz_y$ 。

$P_y$ 更大时也是类似的。得到 $f$ 数组后，我们就容易求出 $g(u,i)$ （how?）。考虑有更多儿子时，其实和两个儿子是类似的，我们先将 $u$ 的前两个儿子的信息合并，再将第三个儿子与前面得到的信息合并，如此往复，就可得到类似的方法。

注意到每次将一个大小为 $x$ 和大小为 $y$ 的信息合并时的复杂度是 $x\times y$ 的，所以总复杂度是 $O(n^2)$ 的。