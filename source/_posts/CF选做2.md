---
title: CF选做2
date: 2023/2/28
description: 　
---

## CF627E

> 在一个 $r \times c$ 的矩阵中有 $n$ 个点，问有多少个连续子矩阵至少包含 $k$ 个点。
> 
> $r,c,n \le 3 \times 10^3$，$k \le 10$。

先枚举上下边界，将其中所有点按照纵坐标排序。

那么答案就是：

$$
\sum_{i}{(y_i-y_{i-1})(c-y_{i+k-1})}
$$

那么固定上边界，在下边界变化的过程中用链表维护答案。

## CF639E

> 有 $n$ 个问题，第 $i$ 个问题的初始得分为 $p_i$，所花费的时间为 $t_i$。
> 
> 设 $T = \sum_{i=1}^n t_i$，你可以按照某个顺序恰好花费 $T$ 时间完成所有问题。
> 
> 若你在时刻 $x$ 完成了问题 $i$，你可以得到 $p_i \cdot (1 - \frac{cx}T)$ 的得分，其中 $c$ 是一个 $[0,1]$ 的实数。
> 
> 对于每个 $c$，都存在至少一个可以使得分最大的最佳做题顺序。
> 
> 对于一个做题顺序，若出现了两个问题 $i,j$ 满足 $p_i < p_j$ 但 $i$ 的得分严格大于 $j$ 的得分，则认为这种做题顺序存在悖论。
> 
> 你需要求出最大的 $c$，使得这个 $c$ 对应的任意最佳做题顺序都不存在悖论。
> 
> $n \le 1.5 \times 10^5$，$p_i,t_i \le 10^8$，答案精度误差 $\le 10^{-6}$。

最优方案一定是按照 $\frac{p}{t}$ 递减排序，用交换法可以证明，每个问题都有最早和最晚被解决的时刻。

于是可以二分 $c$ ，并判断是否存在悖论。

## CF639F

> 给定一张 $n$ 个点 $m$ 条边的初始无向图。
> 
> $q$ 次询问，每次询问给定一个点集 $V$ 和边集 $E$。
> 
> 你需要判断，将 $E$ 中的边加入初始无向图之后，$V$ 中任意两个点 $x,y$ 是否都能**在每条边至多经过一次**的情况下从 $x$ 到 $y$ 再回到 $x$。
> 
> $n,m,q,\sum |V|, \sum |E| \le 3 \times 10^5$，强制在线。

问题等价于 $V$ 中的点是否在一个边双内。

对于原图先求边双，然后缩点，得到森林。

每次询问对每棵树分别求虚树后在跑边双即可。

## CF666D

> 给定平面直角坐标系中的**四个整点**，问是否存在四个整数坐标，满足：
> 第 $1$ 个点能够仅通过竖直**或者**水平移动到达第 $1$ 个坐标（也就是说横坐标或者纵坐标相同），第 $2, 3, 4$ 个点类似。
> 且这四个新的整数坐标形成了面积非负的正方形的四个顶点（也就是说不能重合）。
> 且这个正方形的边必须平行于坐标轴（不是斜着的）。
> 
> 如果存在这样的四个坐标，则尽量最小化对应点移动的距离的最大值。
> （形式化地说，假设第 $i$ 个点移动的距离为 $d_i$，你需要最小化 $\max\limits_{i=1}^{4} d_i$）
> 
> 如果不存在这样的坐标，输出 `-1`。
> 否则输出最小化的 $\max\limits_{i=1}^{4} d_i$，以及那四个坐标。
> 
> 有 $t$ 组询问。

暴力枚举有几个点是横的或竖的即可。

## CF671D

> 给定一棵 $n$ 个点的以 $1$ 为根的树。
> 
> 有 $m$ 条路径 $(x,y)$，保证 $y$ 是 $x$ 或 $x$ 的祖先，每条路径有一个权值。
> 
> 你要在这些路径中选择若干条路径，使它们能覆盖每条边，同时权值和最小。
> 
> $n,m \le 3 \times 10^5$。

方法一：对偶

$\max\{cx|Ax\leq b\}=\min\{b^Ty|A^Ty\geq c^T\}$

www.luogu.com.cn/blog/xzyxzy/solution-cf671d

方法二：直接维护 dp

dfsafdsgaksgh.blog.luogu.org/solution-cf671d

## CF643F

> 有 $n$ 只熊和 $p$ 张床，还有若干个无限大的酒桶（至少一个），其中恰好只有一个酒桶里装着酒，其它酒桶里都装着果汁。
> 
> 熊一开始不知道哪桶里面是酒，于是进行了一次挑战，目标是找到哪桶里面是酒。
> 
> 每天，每只还醒着的熊会选择一个酒桶的子集（可以为空集），并且喝下选择的酒桶中的一小杯饮料。
> 
> 如果一只熊喝到了酒，它会上床睡觉一直到挑战结束。但一张床只能容纳一只熊，如果有熊没有床睡觉，则挑战失败。
> 
> 如果 $i$ 天后至少还剩一只熊没睡觉，且能根据前面的线索推理出哪桶里面是酒，则挑战成功。
> 
> 请你求出对于 $i \in [1,q]$，在可以确保挑战成功的情况下，最多有多少个酒桶。
> 
> 设对于 $i$ 的答案为 $R_i$，你需要求出 $\operatorname{xor}_{i=1}^q ((i \times R_i) \bmod 2^{32})$。
> 
> $n \le 10^9$，$p \le 130$，$q \le 2 \times 10^6$。

信息量。

www.luogu.com.cn/blog/xht37/solution-cf643f

## CF643G

> 给定一个长度为 $n$ 的序列和一个整数 $p$。
> 
> 有 $m$ 个操作，操作要么是区间赋值，要么是询问区间内出现次数至少占 $p\%$ 的数。
> 
> 输出询问的答案时，可以包含错的数，也可以重复输出，但对的数一定要在答案中，且输出的数的个数不超过 $\lfloor \frac{100}{p} \rfloor$。
> 
> $n,m \le 1.5 \times 10^5$，$20 \le p \le 100$。

每次把 $\lfloor \frac{100}{p} \rfloor+1$ 个互不相同的数同时删去，剩下的数就是答案。

用线段树维护每个区间中最多 5 个互不相同的数以及它们的出现次数即可。

## CF679E

> 定义一个正整数是坏的，当且仅当它是 $42$ 的次幂，否则它是好的。
> 
> 给定一个长度为 $n$ 的序列 $a_i$，保证初始时所有数都是好的。
> 
> 有 $q$ 次操作，每次操作有三种可能：
> 
> - `1 i` 查询 $a_i$。
> - `2 l r x` 将 $a_{l\dots r}$ 赋值为一个好的数 $x$。
> - `3 l r x` 将 $a_{l \dots r}$ 都加上 $x$，重复这一过程直到所有数都变好。
> 
> $n,q \le 10^5$，$a_i,x \le 10^9$。

线段树维护每个数到下一个 $42$ 的次幂的差值，暴力更改即可（势能分析）。

## CF685C

> 给定一个立体直角坐标系上的$n$个整点，求一个整点满足到这$n$个整点的曼哈顿距离的最大值最小。
> 
> $1\leq n\leq 10^5,|x_i|,|y_i|,|z_i|\leq 10^{18}$

二分后判断不等式组是否有解。解不等式的过程很妙。

www.luogu.com.cn/blog/chen-zhe/solution-cf685c

## CF698D

> 平面上有 $k$ 个人和 $n$ 个怪物，每个人手中有一支箭。
> 
> 每支箭可以往任意方向射出，击中这个方向上的第一个怪物后，箭和怪物都会消失。
> 
> 问有多少怪物可能会被击中。
> 
> $k \le 7$，$n \le 10^3$。

枚举射击顺序和目标怪物，倒序用队列模拟即可。

## CF700E

> 给定一个字符串 $S$，要求构造字符串序列 $s_1,s_2,\ldots,s_k$，满足任意 $s_i$ 都是 $S$ 的子串，且任意 $i\in[2,n]$，都有 $s_{i-1}$ 在 $s_i$ 中出现了至少 $2$ 次（可以有重叠部分，只要起始、结尾位置不同即可）。
> 
> 求可能的最大的 $k$ 的值（即序列的最大可能长度）。
> 
> $n \leq 2 \times 10^5$。

$s_1,s_2,...,s_k$ 对应着一条 SAM 上从根到叶子路径上的若干节点，考虑 dp 。过程中需要判断父亲节点代表的等价类是否在儿子节点代表的等价类中出现两次，用可持久化线段树维护出每个节点的 endpos 集合即可。

## CF704B

> 有 $n$ 个元素，第 $i$ 个元素有五个参数 $x_i,a_i,b_i,c_i,d_i$。
> 
> 你需要求出一个 $1 \sim n$ 的排列 $p$，满足 $p_1 = s, p_n = e$，同时最小化这个排列的权值。
> 
> 一个排列的权值为 $\sum_{i=1}^{n-1} f(p_i, p_{i+1})$，其中 $f(i,j)$ 的值有两种情况：
> 
> - 若 $i > j$，则 $f(i,j) = x_i - x_j + c_i + b_j$。
> - 若 $i < j$，则 $f(i,j) = x_j - x_i + d_i + a_j$。
> 
> $n \le 5 \times 10^3$，$s \ne e$，$1 \le x_1 < x_2 < \cdots < x_n \le 10^9$，$1 \le a_i,b_i,c_i,d_i \le 10^9$。

贪心神仙题，可以做到 $n\log n$ 。

## CF704C

> 给定 $m$ 个布尔变量 $x_1, x_2, \ldots, x_m$，以及 $n$ 个形如 $x_i$ 或者 $x_i \ \mathrm{or} \ x_j$ 的布尔表达式，其中规定 $x_{-i}=\lnot x_i$。并且，保证 $x_i$ 和 $x_{-i}$ 在所有的布尔表达式中一共只会出现最多两次。
> 
> 请你求出，在一共 $2^m$ 种布尔变量取值的情况下，有多少种情况，使得所有布尔表达式的值的异或为 $1$。此处认为，$\rm True$ 为 $1$，$\rm False$ 为 $0$。
> 
> 由于结果可能过大，请输出答案模 $10^9+7$ 的结果。
> 
> $1 \leq n,m \leq 10^5$。

把表达式看成点，若两个表达式含有相同的变量就连边。

由于题目限制，每个连通块只能是链或者环，都是简单的 dp 。

## CF708D

> 给定一张 $n$ 个点 $m$ 条边的网络，源点为 $1$，汇点为 $n$。
> 
> 对于每条边，有容量 $c$，当前流量 $f$。
> 
> 但这个图是错误的，可能存在 $c < f$，或者流量不守恒的情况。
> 
> 你每次操作可以将某条边的 $c$ 或 $f$ 加 $1$ 或减 $1$。
> 
> 请你用最少的操作次数将图变成一个正确的网络。
> 
> $n,m \le 100$，$c,f \le 10^6$，$1$ 没有入边，$n$ 没有出边。

费用流

www.luogu.com.cn/blog/PinkRabbit/solution-cf708d

## CF708E

> 有一个 $(n+2) \times m$ 的网格。
> 
> 除了第一行和最后一行，其他每一行每一天最左边和最右边的格子都有 $p$ 的概率消失。
> 
> 求 $k$ 天后，网格始终保持连通的概率。
> 
> $n,m \le 1.5 \times 10^3$，$k \le 10^5$，答案对 $10^9+7$ 取模。

容易想到 $n^2m$ 的 dp ，$dp(i,l,r)$ 表示考虑前 $i$ 行，第 $i$ 行剩余格子 $[l,r]$ ，前 $i$ 行联通的概率。转移要求区间有交。

一个经典的技巧是只维护 $F(i)=\sum_{l,r}dp(i,l,r),L(i,x)=\sum_{l,r\leq x}dp(i,l,r),R(i,x)=\sum_{l,r\geq x}{dp(i,l,r)}$ 三个变量即可转移。

## CF1149D

> 一张 $n$ 个点 $m$ 条边的无向图，只有 $a,b$ 两种边权（$a<b$），对于每个 $i$，求图中所有的最小生成树中，从 $1$ 到 $i$ 距离的最小值。
> 
> $n\leq 70,m\leq 200,a,b\leq 10^7$

www.cnblogs.com/7KByte/p/16361166.html