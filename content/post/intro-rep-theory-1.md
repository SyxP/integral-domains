+++
title = "An Introduction to Representation Theory I"

date = 2020-05-13

draft = true

tags = ["math", "representation theory", "algebra", "introduction"]
summary = ""

[header]
image = ""
caption = ""
+++

This is a series of blog posts that plan on covering a topic both extremely elegant
and surprisingly useful. Here, we assume basic familiarity with the notions of groups,
rings, modules, and fields and their morphisms. 
Moreover, all rings will have a multiplicative identity, and ring homomorphisms preserve the identity. 
(I've always wondered why every algebra text states this, since almost all text I've come across assume it.) 

{{% toc %}}

---

## Algebras

Let us begin by discussing a new algebraic structure, so important
that it shares the same name with the subject. 

> **Definition 1** The **centre** of a ring $R$, denoted $Z(R)$, is the set of all elements
in $R$ that commute with every other element in $R$. Symbolically,
>$$Z(R) = \\{a \in R\ |\ ab = ba \forall b \in R\\}$$
> **Definition 2** Let $R$ be a commutative ring, and $A$ a ring. 
\
>Then, an $R$ **-algebra**
is a pair $(A, \rho)$ where $\rho$ is a ring homomorphism from $R \to Z(A)$.

Implicitly, in Definition 2, we have assume that $Z(A)$ is indeed a ring. 
If one wishes to be rigorous, this fact should also be verified. 
Moreover, the map $\rho$ is sometimes clear from context, and we will omit
$\rho$ in the description of an algebra. 

Whenever one has a definition, it is of paramount importance to find as many examples
as one can. Here we shall supply a few.

> **Example 3** Examples of algebras. Here, $R$ denotes a commutative ring
and $\mathbb{k}$ a field.
> 1. Every ring $S$ can be viewed as an $\mathbb{Z}$-algebra. Here, we need a ring homomorphism
$\rho: \mathbb Z \to Z(S)$, and as it must preserve the identity, this can be done in only one way.
Similarly, every $\mathbb Z$-algebra is a ring.
> 2. A polynomial ring $\mathbb k[t_1, t_2, ..., t_n]$ is a $\mathbb k$-algebra with
$\rho$ being the natural inclusion map sending the element $x \in \mathbb{k}$ to the degree 0 polynomial $x \in Z(k[t_1, t_2, ..., t_n])$.
> 3. Group Rings
> 4. Endomorphism Algebra

It is the standard in modern mathematics to treat both the objects and the morphisms between
objects of equal standing.

> **Definition 4** An *homomorphism* of $R$-algebras, $(S, \rho_S)$ and $(T, \rho_t)$, is an homomorphism, $\phi : S \to T$, of the underlying rings, with the additional restriction that $\phi(\rho_S(r)s) = \rho_T(r)\phi(s)$ for all $r \in R$, and $s \in S$.

Let us look with a different perspective. An $R$-algebra, $(S, \rho_S)$, actually also has an $R$-module structure by setting $r\cdot s = \rho_S(r)s$. Often, we would use this notation as well.
The following two exercises showcases the equivalence of the perspectives.

> **Exercise 5** Check that an $R$-algebra is an $R$-module, and an homomorphism of $R$-algebras
is a homomorphism of $R$-modules. 
> **Exercise 6** Show that if $S$ is an $R$-module and a ring, then it can be viewed as an $R$-algebra. Moreover, if an homomorphism of underlying rings between two $R$-algebras happen to 
be a $R$-module homomorphism, then it is an homomorphism of $R$-algebras.

In light of this correspondence, one can give many adjectives to $R$-algebras.
For instance, a **commutative** $R$-algebra, is merely a commutative ring (and a commutative module, but this is a byproduct of the commutativity of the ring). An **ideal** of an $R$-algebra would then be an ideal of the underlying ring and a submodule of the $R$-module, and a $R$ **-subalgebra** is just a subring and a submodule simultaneously.

> **Exercise 7** Define for oneself the **quotient algebra**. Let $S$ be an $R$-algebra and $I$ a
(two-sided) ideal. Then, $S/I$ is also an $R$-algebra.
> **Exercise 8** Play around with the following few adjectives: 
> 1. finite-dimensional, (You may wish to only consider the cases where $R$ is an integral domain or even a field!)
> 2. nilpotent,
> 3. free.
>
> **Exercise 9** Show that direct, free and tensor products of $R$-algebras will give rise to $R$-algebras. (When the author first studied the subject, he was not familiar with the notion of tensor
products. If you're not familiar with it too, you can safely omit it. We will come back to study
tensor products in greater detail.)

---

## Representations

---

Schur's Lemma, Wedderburn-Artin 

---

## Discussion and References

The way this blog post is written is actually a compilation of many results
scattered over various books. The approach is nothing novel, and merely trying
to strike a balance between generalities and ease of understanding. 

I've utilise the following books in the process of creation of this notes.

1. [Pavel Etingof, Oleg Golberg, Sebastian Hensel, Tiankai Liu, Alex Schwendner, Dmitry Vaintrob, and Elena Yudovina - Introduction to Representation Theory](https://bookstore.ams.org/stml-59)
2. [Emmanuel Kowalski - An Introduction to the Representation Theory of Groups](https://bookstore.ams.org/gsm-155/)
3. [Martin Lorenz - A Tour of Representation Theory](https://bookstore.ams.org/gsm-193/)
4. [Alexander Zimmermann - Representation Theory A Homological Algebra Point of View](https://www.springer.com/gp/book/9783319079677)
5. [Ibrahim Assem, Andrzej Skowronski, and Daniel Simson - Elements of the Representation Theory of Associative Algebras, Volume 1: Techniques of Representation Theory](https://www.cambridge.org/core/books/elements-of-the-representation-theory-of-associative-algebras/AA8066B5809D0F556A540400AD3A419C)

Naturally, some commutative algebra books will not be amiss when studying the subject.