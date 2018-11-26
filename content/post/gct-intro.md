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

We begin with a little abstract algebra. Let $G$ be a group, $K$ be a field and $V$ be a finite-dimension (left) $K[G]$-module with dimension $n = \dim(V)$. Let us first stop to recall the definition of a module. A **left $R$-module** on a ring $R$ is an abelian group $(M, +)$ with a left action $\rho : R \times M \to M$ having the following properties:

1. $\rho (r, (x + y)) = \rho (r, x) + \rho (r, y)$,
2. $\rho (r+s, x) = \rho (r, x) + \rho (s, x)$,
3. $\rho (rs, x) = \rho (r, \rho (s, x))$,
4. $\rho (1_R, x) = x$

Without delay, let us see some examples of $R$-modules. We will only discuss left modules as the case for right modules is analogous.

>**Example 1** Let $R$ be a field. Then, $V$ is a $R$-module if and only if $V$ is a $R$-vector space.
\
>**Example 2** For any abelian group $M$ with the action $$\forall k \in \mathbb{Z}\ \forall m \in M, \rho (k, m) = k\cdot m$$ forms a $\mathbb{Z}$-module. Conversely, every abelian group is a module over $\mathbb{Z}$ in a unique, canonical fashion.
\
>**Example 3** Recall that an **ideal** $I$ of a ring $(R, +, \cdot)$ is a subset of $R$ such that $(I, +)$ is a subgroup of $(R, +)$ and $$\forall x \in I\ \forall r \in R, x\cdot r, r\cdot x \in I,$$ in other words, it is an additive subgroup that absorbs multiplication. Here, $I$ is also an $R$-module by setting $$\forall x \in I\ \forall r \in R, \rho (x,r) = x\cdot r.$$


Next, the **group algebra** $K[G]$ is the set of all linear combinations of finitely many elements of $g$, that is, each element can be written as $\sum_{g \in G} a_g g$ where the coefficients $a_i$ lie in $K$. The finiteness conditions restricts all of the coefficients $a_i$ to be zero with finitely many exceptions. This forms an algebra in a straight-forward manner as it satisfies

* $$\sum\_\{g \in G\} a\_g g + \sum\_\{g \in G\} b\_g g =  \sum\_\{g \in G\} (a\_g+b\_g) g,$$
* $$k\sum\_\{g \in G\} a\_g g = \sum\_\{g \in G\} (ka\_g) g,$$
* $$(\sum\_\{g \in G\} a\_g g)\cdot (\sum\_\{g \in G\} b\_g g) = \sum\_\{g,h \in G\} (a\_gb\_h) (g\cdot h).$$

>**Example 4** Let $G$ be a finite cyclic group of order $m$. By writing $G$ as $\\{1,x,x^2,...,x^{m-1}\\}$, we can see that elements of $K[G]$ are actually polynomials of degree $< m$. It is important to note that as $x^m = 1$, we are actually considering the quotient of $K[x]$ by the ideal $\langle x^m - 1\rangle$. In other words, we are taking polynomials of $x$ with coefficients in $K$ modulo $x^m - 1$.
\
>**Example 5** Recall that a **$K$-representation** of a group $G$ is a vector space $V$ over $K$ with a group homomorphism $\phi : G \to Aut(V).$ We shall see that $K[G]$-modules are $K$-representations. Let $V$ be a $K[G]$-module, then our goal is to show that $G$ acts linearly on the $K$-linear vector space $V$. Untangling the definitions, we have a map from the module structure $\rho: K[G] \times V \to V$. Currying this yields $\phi: K[G] \to (V \to V) = Aut(V)$. We can consider the restriction of the input from $K[G]$ to $G$, we can check $\phi|_G$ is indeed a invertible linear map, and hence a group representation. The converse also holds as the action by $G$ induces a unique action by $K[G]$.

You should read Example 5 as saying $K$-representations and $K[G]$-modules are equivalent, with slight abuse of notation, we shall treat $V$ as a $K$-representation. Moreover, this allows us to define what we meant when we claim that $V$ has dimension $n$. We can view it as a $K$-representation into a vector space $V$ which has dimension $n$ over $K$. 

Be very careful on the next part as the notation is potentially very confusing! Let $k[V]^G$ denote the **invariant ring** of $V$ by action of $G$ (note that $V$ is a vector space over $K$ and not a group and hence $K[V]$ is not a group ring). I shall give an alternative description as the notation is meant for a more abstract concept and would not be needed in the current discussion. (Namely, we can take $V$ to be any affine variety, and $K[V]$ to be its coordinate ring. However, this does not interest us as of now as when we consider representation varieties, $V$ is always a vector space.) 

We can choose a basis of $V$, explicitly $x_1, x_2, ..., x_n$. Then we can construct the set of all finite degree polynomials with coefficients in $K$. This would denote the **coordinate ring** $K[V]$ for our purposes. Then, as $G$ acts on $V$ (as a $K$-representation), it induces an action on $K[V]$, $K[V]^G$ is merely the set of invariant polynomials under the action of $G$. Now let us be very explicit in the following example which will (hopefully) clarify the situation.

>**Example 6** Let $G$ be the group of two elements $\\{e, s\\}$ where $s^2 = e$, $K = \mathbb{C}$ and $V$ be the $K$-representation with $V = \mathbb{C}^2$ and $\phi$ satisfying:
\
>$$\phi(e) = \begin{pmatrix} 1 & 0 \\\\ 0 & 1 \end{pmatrix},$$
>$$\phi(s) = \begin{pmatrix} 0 & -1 \\\\ -1 & 0 \end{pmatrix}.$$
\
> We start by picking a basis of $K$, namely $x = (1\ 0)^T$ and $y = (0\ 1)^T$. First, we ask what is $K[V]$, this is merely set of polynomials in $x,y$ with coefficients in $\mathbb{C}$. In other words, $K[V] = \mathbb{C}[x,y]$. Next, we wish to know the action of $G$ via $\phi$. We have $\phi(s)(x) = -y$ and $\phi(s)(y) = -x$. We first say $\phi(s)$ induces an action on $K[V]$, e.g. $$\phi(s)(x^2 + 3y) = (-y)^2 + 3(-x) = y^2 - 3x.$$Now $K[V]^G$ is the set of polynomials invariant under this action. For instance $x^2 + 3y$ is not invariant as $x^2 + 3y \neq y^2 - 3x$ but $xy, x^3y + y^3x, 2i$ are all invariant. It turns out that all such polynomials are polynomials of $xy$ and $x^2 + y^2$. Equivalently, we can write $K[V]^G = \mathbb{C}[xy, x^2+y^2]$.

A thorough understanding of Example 6 is strongly recommended before continuing. Here, we have concluded the set up. The basic premise is that we are given $G$ and $V$, and we have to answer questions regarding $K[V]^G$ within polynomial (efficient) time. A small caveat is that this is dependent on the way we have chosen to denote $V$. It turns out we can encode the input in $poly(n,m)$ bits. This is fairly technical and although an efficient encoding of $V$ is vital to the efficiency of any subsequent algorithm, this is not our focus for this discussion, and the author has chosen to omit it.

Returning to Example 6, we can see that $K[V]^G$ in that case can be generated by two elements, namely $xy$ and $x^2 + y^2$. The first problem of invariant theory actually asks when a finite basis exists and if it is finite (we say that the invariant ring is finitely generated), explicity (this is used informally here) write down a basis. The reader might choose to amuse themselves with other small groups and their representations.

From this point onwards, we will fix $G = SL_m(\mathbb{C})$ and $K = \mathbb{C}$, except when explicitly stated otherwise, even though the results may hold more generally. 
