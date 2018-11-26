+++
title = "Geometric Complexity Theory - An Introduction"

date = 2018-11-26

draft = false

tags = ["math", "alggeom", "compsci", "complexity"]
summary = "An introduction to Geometric Complexity Theory (GCT) without heavy mathematical machinery. We will discuss the key ideas in GCT and apply it to investigating the Polynomial Identity Testing problem."

[header]
image = ""
caption = ""
+++

Since 1999, Mulmuley and his collaborators devised an innovative approach to tackle problems in algebraic complexity. However, this topic assumes substantial mathematical maturity and could be fairly impenetrable otherwise. In today's discussion, the author hopes to explore a small fraction of the work that has been done in this program, while avoiding the use of heavy mathematical machinery. The discussion here will be primarily be based on \[[Mulmuley GCT V](https://arxiv.org/abs/1209.5993)\]. A key difference from other introductions is the focus on Polynomial Identity Testing, this is an attempt to motivate the discussion. Finally, we will (unfortunately) not be stating the results in full generality, which should aid in understanding.

---

Let $G$ be a group, $K$ be an algebraically closed field and $V$ be a finite-dimension (left) $K[G]$-module with dimension $n = \dim(G)$. Let us first stop to recall the definition of a module. A **left $R$-module** on a ring $R$ is an abelian group $(M, +)$ with a left action $\rho : R \times M \to M$ having the following properties:

1. $\rho (r, (x + y)) = \rho (r, x) + \rho (r, y)$,
2. $\rho (r+s, x) = \rho (r, x) + \rho (s, x)$,
3. $\rho (rs, x) = \rho (r, \rho (s, x))$,
4. $\rho (1_R, x) = x$

Without delay, let us see some examples of $R$-modules. We will only discuss left modules as the case for right modules is analogous.

>**Example 1** Let $R$ be a field. Then, $M$ is a $R$-module if and only if $M$ is a $R$-vector space.
\
>**Example 2** For any abelian group $M$ with the action $$\forall m \in M, \rho (k, m) = k\cdot m$$ forms a $\mathbb{Z}$-module. Conversely, every abelian group is a module over $\mathbb{Z}$ in a unique, canonical fashion.
\
>**Example 3** Recall that an **ideal** $I$ of a ring $(R, +, \cdot)$ is a subset of $R$ such that $(I, +)$ is a subgroup of $(R, +)$ and $$\forall x \in I\ \forall r \in R, x\cdot r, r\cdot x \in I,$$ in other words, it is an additive subgroup that absorbs multiplication. Here, $I$ is also an $R$-module by setting $$\forall x \in I\ \forall r \in R, \rho (x,r) = x\cdot r.$$


Next, we shall discuss representations and group rings. A **representation** of $G$ is a vector space $V$ over $K$ with a group homomorphism $\phi : G \to Aut(V).$ Then the **group ring** $K[G]$ is defined by 
