+++
title = "Cluster Algebras"

date = 2020-09-11

draft = false

tags = ["math", "representation theory", "algebra", "introduction"]
summary = "An example-based introduction to Cluster Algebras"

[header]
image = ""
hattion = ""
+++


Our goal today is to understand what a Cluster Algebra is. 

{{% toc %}}

---

## Grassmannian Varieties

We begin our story with studying the **Grassmannian**. 

> **Definition 1** The Grassmannian $Gr_{k, n}$ is the set of all $k$-dimensional 
> subspaces of $\mathbb{R}^n$, where $1 \leq k \leq n-1$.
>
> *Remark* : We could do this over any field, but here we used $\mathbb R$ for convenience.

Let us illustrate what exactly $Gr_{1,2}$ is. Here, we need to consider a $1$-dimensional subspace of $\mathbb{R}^2$, which can be thought of a line passing through the origin. 

$$ \begin{align*} 
Gr_{1,2} &= \\{\\{\lambda v\ |\ \lambda \in \mathbb{R}\\}\ |\ v \in \mathbb C\\} \\\\
\end{align*}$$

However, we could send each line $\\{\lambda v\\}$ to the point $\frac{v}{||v||}$. This gives us an identification with the upper half semi-circle in $\mathbb{R}^2$ (which one could also think as related to $\mathbb{R}P^1$). We could attempt to do this more generally. Let us choose a basis of $\mathbb{R}^n$, say $e_1, e_2, ..., e_n$. Then a line is simply the set of points $\\{\lambda v\ |\ \lambda \in \mathbb R\\}$ for a vector $v = \sum_i v_ie_i$.

Hence for the elements of $Gr_{k,n}$, we have a subspace of dimension $k$ which is the same as the span $k$ linear independent vectors, and yield a sum $v_k = \sum_i v_{k,i}e_i$, and we can denote this with a matrix as follows,

$$\begin{pmatrix}
v_{1,1} & v_{1,2} & v_{1,3} & \dots & v_{1,n} \\\\
v_{2,1} & v_{2,2} & v_{2,3} & \dots & v_{2,n} \\\\
\vdots & \vdots & \vdots  & \ddots & \vdots \\\\
v_{k,1} & v_{k,2} & v_{k,3} & \dots & v_{k,n}
\end{pmatrix}.$$

Let us denote the $i$-th column of such a matrix $U$ as $\hat U_i$. For a slight abuse of notation, when given an element of $U \in Gr_{k,n}$, we will still write $\hat{U}_i$.

{{% alert warning %}}
Note that the elements of $Gr_{k,n}$ are subspaces, and two different matrices can have the same span, and hence be the same element. In particular, we can swap any two rows, multiply any row with a non-zero constant and add a row to another. 

In other words, we can consider the set of full rank $k$ by $n$ matrices modulo the action of $GL_k(\mathbb{R})$.
{{% /alert %}}

> **Notation 2** We shall denote the set of numbers $\\{1,2,3,...,N\\}$ as $[n]$.
> **Definition 3** We have the natural **Plücker map** from $Gr_{k,n}$ to $P(\bigwedge^k \mathbb{R}^n)$.
> It suffices to determine the value on the natural basis of $P(\bigwedge^k \mathbb{R}^n)$.
> For each subset of size $k$ of $[n]$, $C = \\{c_1, c_2, ..., c_k\\}$ where $c_1 < c_2 <  ... < c_k$, we send $U \in Gr_{k,n}$ to
> $$\Delta_C(U) = \textrm{det}\begin{pmatrix} | & | &  & | \\\\
\hat{U}_{c_1} & \hat{U}_{c_2} & \dots & \hat{U}_{c_k} \\\\
| & | &  & | \end{pmatrix}$$.

We will also denote this as $\Delta: Gr_{k,n} \to P(\bigwedge^k \mathbb{R}^n)$ and the component functions as $\Delta_C$. Recall by the above warning that we have to check that this is indeed well-defined.

> **Exercise 4** Check that the Plücker map is well-defined. More precisely, let $U$ be a full rank $k$ by $n$ matrix and $T \in GL_k(\mathbb{R}).$ Then check for any two subsets $A, B \subseteq [n]$ of size $k$, $\frac{\Delta_A(U)}{\Delta_B(U)} = \frac{\Delta_A(TU)}{\Delta_B(TU)}$.

The first surprising result today is that this Plücker map is actually injective.

> **Theorem 5** The Plücker map $\Delta$ is injective.
\
> **Proof** Let $U$ and $V$ be two matrices representing two elements of $GL_k(\mathbb{R})$ such that $\Delta(U) = \Delta(V).$
\
> Suppose there exists a $A \in [n]$ such that $\Delta_A(U)$ and $\Delta_A(V)$ are non-zero. (If no such $A$ exist, then $U = V = 0.$) Without loss of generality, we can assume that when restricted to the columns indexed by $A$, $U$ and $V$ are both the identity matrix. This is as we can find $S, T \in GL_k(\mathbb R)$ and consider $U' = SU$ and $V' = TV.$
\
> However, let $a = \\{a_1, a_2, ..., a_k\\}$ where $a_1 < a_2 < ... a_k$ and $U_{ij}$ and $V_{ij}$ be the $(i,j)$-th entry of $U$ and $V$ respectively. Then, for any $1 \leq i \leq k$ and $1 \leq j \leq n$, 
> $$ \begin{align*} 
 U_{ij} &= \mathrm{det}\begin{pmatrix} | & | &  & | & | & |& &|\\\\
\hat{U}_{a_1} & \hat{U}_{a_2} & \dots & \hat{U}_{j-1} & \hat{U}_i &\hat{U}_{j+1} & \dots & \hat{U}_{c_k} \\\\
| & | &  & | & | & |& &|\end{pmatrix} \\\\
&= (-1)^r \Delta_{A\setminus \\{j\\} \cup \\{i\\}}(U) \\\\
&= (-1)^r \Delta_{A\setminus \\{j\\} \cup \\{i\\}}(V) \\\\
&= \mathrm{det}\begin{pmatrix} | & | &  & | & | & |& &|\\\\
\hat{V}_{a_1} & \hat{V}_{a_2} & \dots & \hat{V}_{j-1} & \hat{V}_i &\hat{V}_{j+1} & \dots & \hat{V}_{c_k} \\\\
| & | &  & | & | & |& &|\end{pmatrix}
= V_{ij},
\end{align*}$$ 
> where $r$ is some fixed integer.


Next, we shall focus on the case where $k = 2$. The following theorems are true in general, but let us not be too ambitious today. 

> **Notation 6** We shall write $\Delta_{ij}$ to mean $\Delta_{\\{i,j\\}}$. For instance, $\Delta_{12}$ will refer to $\Delta_{\\{1,2\\}}$.

Let us observe that $\Delta_{12}\Delta_{34} + \Delta_{14}\Delta_{23} = \Delta_{13}\Delta_{24}.$ (This is an equality as functions on $\mathrm{Hom}(Gr_{2,n},\mathbb{R})$) More generally, for any $1 \leq a < b < c < d \leq n$, $$\Delta_{ab}\Delta_{cd} + \Delta_{ad}\Delta_{bc} = \Delta_{ac}\Delta_{bd}.$$

These are known as **Plücker relations**. To justify the name in this section of the Grassmannian *variety*, the following theorem should not come as a surprise.


> **Exercise 7** Show that the Plücker relations hold. (It suffices to check $\Delta_{12}\Delta_{34} + \Delta_{14}\Delta_{23} = \Delta_{13}\Delta_{24}$) 
>
> **Theorem 8** The Grassmannian $Gr_{2,n}$ is the zero set of the Plücker relation polynomials.
>
> **Proof** Exercise 7 gives us one direction.
> For the reverse containment, let us pick a point $q \in P(\bigwedge^2 \mathbb{R}^n)$, where the $(i,j)$-th projective component where $i < j$ is $q_{ij}$. Without loss of generality, let $q_{12} = 1$. Then, let 
>$$U = \begin{pmatrix} q_{12} & 0 & q_{23} & q_{24} & \dots & q_{2n} \\\\ 
0 & q_{12} & q_{13} & q_{14} & \dots & q_{1n} \end{pmatrix}.$$
> The full rank of $U$ follows as the first two columns is an identity matrix. 
> Moreover, $\Delta_{ij}(U) = q_{2i}q_{1j} - q_{2j}q_{1i} = q_{12}q_{ij} = q_{ij}$ and $\Delta(U) = q.$

---
## Totally Positive Grassmannian

Next, we move on to discuss the notion of a total positivity. 

---
**Acknowledgements**

For the initial section of the Grassmannian, I referenced [Lakshmibai and Brown's Flag Varieties](https://link.springer.com/book/10.1007/978-93-86279-41-5).