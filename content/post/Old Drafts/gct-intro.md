+++
title = "Geometric Complexity Theory - An Introduction"

date = 2018-11-26

draft = true

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

Be very careful on the next part as the notation is potentially very confusing! Let $K[V]^G$ denote the **invariant ring** of $V$ by action of $G$ (note that $V$ is a vector space over $K$ and not a group and hence $K[V]$ is not a group ring). I shall give an alternative description as the notation is meant for a more abstract concept and would not be needed in the current discussion. (Namely, we can take $V$ to be any affine variety, and $K[V]$ to be its coordinate ring. However, this does not interest us as of now as when we consider representation varieties, $V$ is always a vector space.) 

We can choose a basis of $V$, explicitly $x_1, x_2, ..., x_n$. Then we can construct the set of all finite degree polynomials with coefficients in $K$. This would denote the **coordinate ring** $K[V]$ for our purposes. Then, as $G$ acts on $V$ (as a $K$-representation), it induces an action on $K[V]$, $K[V]^G$ is merely the set of invariant polynomials under the action of $G$. Now let us be very explicit in the following example which will (hopefully) clarify the situation.

>**Example 6** Let $G$ be the group of two elements $\\{e, s\\}$ where $s^2 = e$, $K = \mathbb{C}$ and $V$ be the $K$-representation with $V = \mathbb{C}^2$ and $\phi$ satisfying:
\
>$$\phi(e) = \begin{pmatrix} 1 & 0 \\\\ 0 & 1 \end{pmatrix},$$
>$$\phi(s) = \begin{pmatrix} 0 & -1 \\\\ -1 & 0 \end{pmatrix}.$$
\
> We start by picking a basis of $V$, namely $x = (1\ 0)^T$ and $y = (0\ 1)^T$. First, we ask what is $K[V]$, this is merely set of polynomials in $x,y$ with coefficients in $\mathbb{C}$. In other words, $K[V] = \mathbb{C}[x,y]$. Next, we wish to know the action of $G$ via $\phi$. We have $\phi(s)(x) = -y$ and $\phi(s)(y) = -x$. We first say $\phi(s)$ induces an action on $K[V]$, e.g. $$\phi(s)(x^2 + 3y) = (-y)^2 + 3(-x) = y^2 - 3x.$$Now $K[V]^G$ is the set of polynomials invariant under this action. For instance $x^2 + 3y$ is not invariant as $x^2 + 3y \neq y^2 - 3x$ but $xy, x^3y + y^3x, 2i$ are all invariant. It turns out that all such polynomials are polynomials of $xy$ and $x^2 + y^2$. Equivalently, we can write $K[V]^G = \mathbb{C}[xy, x^2+y^2]$.

A thorough understanding of Example 6 is strongly recommended before continuing. Here, we have concluded the set up. The basic premise is that we are given $G$ and $V$, and we have to answer questions regarding $K[V]^G$ within polynomial (efficient) time. A small caveat is that this is dependent on the way we have chosen to denote $V$. It turns out we can encode the input in $poly(n,m)$ bits. This is fairly technical and although an efficient encoding of $V$ is vital to the efficiency of any subsequent algorithm, this is not our focus for this discussion, and the author has chosen to omit it.

Returning to Example 6, we can see that $K[V]^G$ in that case can be generated by two elements, namely $xy$ and $x^2 + y^2$. The first problem of invariant theory actually asks when a finite basis exists and if it is finite (we say that the invariant ring is finitely generated), explicity (this is used informally here) write down a basis. The reader might choose to amuse themselves with other small groups and their representations.

From this point onwards, we will fix $G = SL_m(\mathbb{C})$ and $K = \mathbb{C}$, except when explicitly stated otherwise, even though the results may hold more generally.

We start by the key insight of succinctness. It turns out that the problem as we have stated will always have a finite set of generators, however, it could have exponentially many of them. This is not a good sign, as it would suggest that there is no polynomial time algorithm for ${\rm G{\small ENERATORS}}$. The insight here is to change our notion of what we consider a suitable answer to the problem.

In the spirit of \[[Wilf 1982](https://www.jstor.org/stable/2321713)\], the notion of computational complexity will come into our closed form. Instead of asking to list out such a basis, we express them as follows.

The ring of invariants $K[V]^G$ has a set of generators with  **succinct encoding** if there exists an algebraic circuit $C = C[V,m]$ with rational constants of at most $poly(n,m)$ bit-size over the coordinates $v = (v\_1,...,v\_n)$ of $V$ and auxillary variables $y = (y\_1,...,y\_k)$ and $k$ is at most $poly(n)$, satisfying: $$C(v,y) = \sum_\mu f\_\mu(v)\mu(y),$$ where $\mu$ are monomials in the auxillary variables $y$, $f\_\mu(v) \in K[V]^G$ and $f\_\mu(v)$ generates $ K[V]^G$.

This could be seen as a "generating-function" of the generators (no pun intended). Here, we can have exponentially many generators, but yet succinctly output them with small output size. It is not hard to see that if you have finitely many generators, this would also be considered a succint encoding.

What is the status of this problem? Well we have the following theorem.

>**Theorem 7** \[[Mulmuley GCT V](https://arxiv.org/pdf/1209.5993.pdf#subsection.8)\] For fixed $m$, then ${\rm G{\small ENERATORS}} \in NC$.
\
>**Proof** See Theorem 8.1 (or Theorem 8.5). (Highly nontrivial) The best known case for general $m$ is found in Theorem 9.7. Special cases for general $m$ are also known. For instance, when $V = K^m \oplus K^m ... \oplus K^m$ ($r$ times) results from \[[Weyl 1936 Theorem 2.6 A](https://www.jstor.org/stable/j.ctv3hh48t)\].

Finally, we can see a link to the white-box Polynomial Identity Testing (PIT). White-box PIT is the problem where given a description of an algebraic circuit, we wish to determine if the polynomial encoded by this circuit is identically zero.

We can define the **null cone** $N(V) \subseteq V$ as the set of points $v \in V$ where there exists a $g \in G$ such that $g \cdot v$ is the origin of $V$. Then the Null Cone Membership Problem (NCMP) is that given $(V,G)$ and a rational point $v$, determine in $v$ lies in $N(V)$.

We end with the following link.

>**Theorem 8** \[[Mulmuley GCT V](https://arxiv.org/pdf/1209.5993.pdf#subsection.7.4)\] NCMP is in $P$ if 
${\rm G{\small ENERATORS}}$ is in $P$ for arbitrary $m$ and white-box PIT is in $P$.
\
>**Proof** Derandomize Theorem 7.8 via Theorem 7.9.

Unfortunately, we would really like to say the converse, but this requires the consideration of a more general variety then $K[V]^G$ (namely $\Delta\[\text{det},m\]$). Here, we barely scratch the surface of what the GCT program has covered, and hopefully I have given a glimpse of what the program has to offer.
