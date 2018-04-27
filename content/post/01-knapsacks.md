+++
title = "0-1 Knapsacks"

date = 2018-01-25T00:00:00
lastmod = 2018-01-25T00:00:00
draft = false

tags = ["compsci", "knapsack"]
summary = "Investigating the 0-1 Knapsack problem."

[header]
image = ""
caption = ""
+++

You have $N$ items, the $i$-th item having integer weight $w\_i \in \mathbb{N}$ and integer value $v\_i \in \mathbb{N}$, and a bag with carrying capacity $B$. Your goal is to take items such that their value is maximized, but their weight cannot exceed the carrying capacity of the bag. In other words, find a subset $S \subseteq \\{1,2,...,N\\}$ such that $\sum\_{i \in S} v\_i$ is maximized subject to $\sum\_{i\in S} w\_i \leq B$.

This is known as **0-1 knapsack problem**. Naïvely, by trying all the subsets, we can derive a $ \Theta(N\cdot 2^N) $ algorithm. This can be sped up by a factor of $ \Theta(N) $ by considering a Gray code. In light of the following algorithm, we shall not discuss this in greater detail.

>**Algorithm 1** \[[Horowitz and Sahni 1974](https://dl.acm.org/citation.cfm?id=321823)] The 0-1 knapsack problem can be solved in $\Theta(N\cdot 2^\frac{N}{2}) $ time.
\
>**Proof** Let $I = \\{1,2,...,\frac{N}{2}\\}$ and $J = \\{\frac{N}{2}+1,\frac{N}{2}+2,...,N\\}$. For each $X \subseteq I$, it suffices to find $Y \subseteq J$ such that $\sum\_{i\in Y} v\_i$ is maximized subject to $\sum\_{i\in Y} w\_i \leq B - \sum\_{i\in X} w\_i$. This can be done efficiently by sorting the set $\\{(\sum\_{i\in Y} w\_i, \sum\_{i\in Y} v\_i) | Y \subseteq J\\}$, reducing the problem to a query on the maximum value of $v\_i$ of a prefix of the sorted set. 

The above technique is also known as "meet in the middle". Generally, we have a set $S$ and wish to determine a subset $X \subseteq S$ with some property. This is done by partitioning $S$ into two sets $I,J$. By enumerating all subsets of $I$ and $J$, this would take $\Theta(|2^I| + |2^J|)$ time. For the technique to succeed, we hope to combine the partial results on $I' = 2^I$ and $J' = 2^J$ more efficiently than quadratic time (i.e. $o(|I'|\cdot |J'|)$), resulting in an algorithm in $o(|2^S|)$ time. Often, this step is done via a combination of sorting and binary search.

>**Problem 2** Can we do better than $\Theta(N\cdot 2^\frac{N}{2})$ time?
\
>Hint: Perform a different enumeration of the subsets of $I$ and $J$.
>
>**Problem 3** Can we do better than $\Theta(2^\frac{N}{2})$ time?
>
>**Problem 4** \[[Andrew Rayskiy](http://codeforces.com/problemset/problem/478/E)\] Given $S$, a set of prime numbers, and $N\in \mathbb{N}$. Determine the number of distinct $k \in \\{1,2,...,N\\}$ with the property that every prime factor of $k$ is in $S$.

A natural question to ask is does there exists a polynomial time algorithm for the 0-1 knapsack problem. 

>**Theorem 5** \[[Karp 1972](https://link.springer.com/chapter/10.1007/978-1-4684-2001-2_9)\] Unless ${\rm P} = {\rm NP}$, there does not exist a polynomial time algorithm for 0-1 knapsack.
>
>**Problem 6** Consider the **subset sum problem**: Given a set $S \subset \mathbb{Z}$, is there a subset $I \subseteq S$ that sums to 0 (i.e. $\sum\_{i \in I} i = 0$)? Give a polynomial time reduction from 3-satisfiability to subset sum, then a polynomial time reduction from subset sum to 0-1 knapsack. Hence or otherwise, show Theorem 5.

That's disappointing. The 0-1 knapsack problem is unlikely to admit a polynomial time solution. For ${\rm NP}$-complete problems, we should look towards special cases where it is possible to solve the problem quickly.  We could make the following observation when $B$ is small.

>**Algorithm 7** The 0-1 knapsack problem can be solved in $\Theta(N\cdot B)$ time.
\
>***Proof*** Define $f(k,C)$ as the solution to the 0-1 knapsack problem of the first $k$ items and a bag with carrying capacity $C$. Note that 
>
> * It suffices to compute $f(N,B)$,
>
> * For all values of $C \in \mathbb{N}$, $f(0,C) = 0 $, and
>
> * $ f(k,C) = \max(f(k-1,C),f(k-1,C-w\_k) + v\_k) $.

This is not the only special case with an efficient solution. For example, if $v\_i \geq v\_{i+1}$ and $w\_i \leq w\_{i+1}$ for all $i \in \\{1,2,...,N-1\\}$, there is a linear time greedy solution. Another instance we can improve on Algorithm 7 is when we have only $C\_w$ distinct weights. Here, there is a $\Theta(B \log{C\_w}\cdot (B + \log{N}))$ algorithm. The following problems give a few more variations.

>**Problem 8** Let $L = \sum_{i=1}^N v_i$. Show that the 0-1 knapsack problem can be solved in $\Theta(N\cdot L)$ time.
>
>**Problem 9** \[[Evgeny Zamyatin](http://neerc.ifmo.ru/school/io/archive/20150330/problems-20150330-individual.pdf#page=4)\] Given a multiset $S$ of positive integers with sum $\sum\_\{i \in S\} i = N $, determine efficiently if you can partition $S$ into two disjoint subsets $I,J$ such that they have equal sum (i.e. $\sum\_\{i \in I\} i = \sum\_\{i \in J\} i$).
>
>**Problem 10** \[[Gennady Korotkevich](https://agc020.contest.atcoder.jp/tasks/agc020_c)\] Given a multiset $S$  of positive integers with the $i$-th element $S\_i \leq N$, determine efficiently the median of the multiset $\\{\sum\_\{i \in I\} i\ |\ I \subseteq S, I \neq \emptyset\\}$.
>
>**Problem 11** Determine special cases of $(c_i, v_i)$ where we can have an improvement over Algorithms 1 and 7.
