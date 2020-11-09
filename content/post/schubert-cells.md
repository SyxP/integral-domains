+++
title = "Grassmannian, Flag Varieties and Schubert Cells"

date = 2020-11-09

draft = false

tags = ["math", "representation theory", "algebra", "introduction"]
summary = "Understanding Schubert Cells"

[header]
image = ""
caption = ""
+++

The theory of algebraic groups has been rather scattered during my experience of learning it.
Today, we will try and compile the various resources, and attempt to translate back and forth
between the various vocabularies one would encounter when attempting to study the topic.

{{% toc %}}

---
## What's in an Algebraic Group?

Our first goal is to understand what objects we wish to study, namely the **algebraic groups**.
But before that, we should first roughly guess what objects should fit under said label, which will in
turn inform us on how general a definition we should use. Indeed, there would be many paradigms and definitions when studying algebraic groups, not all equivalent, which differ based on how much generality you wish to use. 

> **Definition 1A** Consider the group $G = GL(n, \mathbb C)$ with as a topological (Lie) group.
> A group $H \subseteq G$ is a **matrix Lie group** if $H$ is a closed subgroup of $G$.

Often times, the adjectives *matrix Lie* suffices as a stand-in for *algebraic*, especially when one is only concerned over the groups in $\mathbb C$ or $\mathbb R$. Importantly, even when one works with full generality of algebraic groups, having stereotypical examples of them is essential to giving us "test cases" to quickly check the importance or validity of various theorems. Indeed, these are a very large class of examples.

>**Example 2** Every Finite Group is a matrix Lie group. This is as every finite group is a subgroup
> of the symmetric group $\mathfrak S_n$ by Cayley's Theorem, which in turn is a closed subgroup of $GL(n, \mathbb C)$.

This are actually the nasty cases of the theory of algebraic groups. We will often demand that our groups be connected, just to avoid the montrosities of finite group theory invading the theory of algebraic groups. Surprisingly, the latter is far more well-behaved than the former. To motivate this,
we shall define the following.

> **Definition 2A** A matrix Lie group $G$ is **connected** if it is connected in its underlying topology. For any matrix Lie group $G$, we denote that component containing the identity element $\mathrm{C_e}(G)$.

Before we move on, we should look at some examples of connected matrix Lie groups.

>**Example 3** (Type A) The groups $SL(n, \mathbb k)$ and $GL(n, \mathbb k)$ are connected matrix Lie group for $\mathbb k$ equal to $\mathbb R$ or $\mathbb C$. The former are the elements in $GL(n, \mathbb k)$ with determinant $1$.
\
>**Example 4** (Type D) The special orthogonal group $SO(2n, \mathbb k)$ consists of the elements $A \in GL(n, \mathbb k)$ such that $A^\dagger A = \mathrm{Id}_n$ where $\mathbb k$ equal to $\mathbb R$ or $\mathbb C$. Note that if $k = \mathbb R$, then there would be two connected components, so we need to take the connected component together with the identity.


It is natural here to continue with the various real and complex Lie groups corresponding to the different Dynkin diagrams. For brevity, We shall omit explicitly writing this out.
There full classification of matrix Lie groups over the complex numbers can be found in any textbook on Lie theory,
for example [\[Humphreys, 1\]]({{<ref "#acknowledgements" >}}) or [\[Bump, 2\]]({{<ref "#acknowledgements" >}}).
More surprisingly may be the following examples.

>**Example 5** (Projective Special Linear Group) We can take the matrix Lie group $G = SL(n, \mathbb k)$ as per Example 3, and consider $PSL(n, \mathbb k) = G/\mathrm{Z}(G)$ where $\mathrm Z(G)$ denotes the centre of the group.
> It is not immediately clear that this is a closed subgroup of $GL(n, \mathbb C)$, and indeed it is not, but it is a closed subgroup of $GL(n^2, \mathbb C)$!
\
>**Exercise 6** Show that $PSL(n, \mathbb k)$ is a closed subgroup of $GL(n, \mathbb C)$. Are these group connected? (Hint: For the first part, show that $PGL_n \to \mathrm{Aut}(\mathrm{Mat}_n)$ is a group isomorphism and apply Skolem-Noether. For the second part, use either Iwasawa or QR Decomposition)

Before moving on from these examples, it would also be informative to understand why we restrict to matrix Lie groups and not Lie groups in general. The following warning has caused the author to be greatly perplexed before they had realised.

{{% alert warning %}}
Later, we will see more definitions of affine algebraic (or reductive) groups. Lie groups in general are not affine algebraic groups! For example, consider the universal cover of $SL(2, \mathbb R)$
or the metaplectic group, which is the double cover of the symplectic group $Sp(2, \mathbb R)$. (The latter has the Lie algebra $\mathfrak{sl}(2, \mathbb R)$) Neither of these have faithful finite-dimensional matrix representations, and would not be considered algebraic! Of note, the metaplectic group actually has a representation with finite kernel.

On the other hand, the Spin group $\mathrm{Spin}(n, \mathbb R)$ which are double covers of $SO(n,\mathbb R)$ are actually matrix Lie groups, but the smallest faithful representations have a high dimension. See [\[Borcherds 3, Lectures 2 - 3\]](https://math.berkeley.edu/~reb/courses/261/) for more detail.
{{% /alert %}}

----
## Acknowledgements

Many notes and books were referenced throughout the notes. I attempted to group them by group of topics.
First, the references for Lie theory.

1. [James Humphreys - Introduction to Lie Algebras and Representation Theory](https://www.springer.com/gp/book/9780387900537)
2. [Daniel Bump - Lie Groups](https://www.springer.com/gp/book/9781475740943)
3. [Lecture notes by Richard Borcherds](https://math.berkeley.edu/~reb/courses/261/)