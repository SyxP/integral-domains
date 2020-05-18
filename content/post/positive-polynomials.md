+++
title = "Positive Polynomials"

date = 2020-05-19

draft = false

tags = ["math", "analysis", "polynomials"]
summary = ""

[header]
image = ""
caption = ""
+++

I've recently chanced upon this beautiful theorem and I just have to share it.

> **Definition 1** A polynomial $p : \mathbb{R}^n \to \mathbb{R}$ with real coefficients is called
> * **positive** if $p(v) > 0$ for all $v \in \mathbb{R}^n$,
> * **non-negative** if $p(v) \geq 0$ for all $v \in \mathbb{R}^n$.

How would we check if a given polynomial is positive or non-negative? Let us recall the technique of 
completing the square. If $p \in \mathbb{R}[x]$ is a quadratic polynomial, say $p(x) = ax^2 + bx + c$,
then we can rewrite it as
$$\begin{align}
p(x) &= a\left(x + \frac{b}{2a}\right)^2 + \left(c - \frac{b^2}{4a}\right) \\\\
&\geq c - \frac{b^2}{4a}\end{align}.$$

This allows us to check if a quadratic is a positive polynomial. Surprisingly, we can do the same for any
polynomial in $\mathbb{R}[x]$.

> **Theorem 2** Let $p \in \mathbb{R}[x]$, then $p$ is non-negative if and only if
there exists $f,g \in \mathbb{R}[x]$ such that $p = f^2 + g^2.$
---
If $p$ is really of the form $f^2 + g^2$, then it must be the case that it is non-negative. We shall concentrate
our efforts to show the other direction. But first, we need to establish a few lemmas on the nature of roots
of non-negative polynomials.

> **Lemma 3** Let $p \in \mathbb{R}[x]$ be a non-negative polynomial and $a$ be a real root. Then
we can find $q \in \mathbb{R}[x]$ such that $p(x) = (x-a)^2q(x)$.
\
> **Proof** By the polynomial remainder theorem, we can find $m \in \mathbb{R}[x]$
such that $p(x) = (x-a)m(x)$. If $m(a) = 0$, then we can find $q \in \mathbb{R}[x]$
so $m(x) = (x-a)q(x)$ and we have our result.
>
> So let us suppose that $m(a) \neq 0$. Then there exists an $\epsilon > 0$ such that
> $(a - \epsilon, a + \epsilon)$, the polynomial $m$ has no roots, and thus by intermediate
> value theorem, $m(a - \epsilon)$ and $m(a + \epsilon)$ share the same sign. 
> But then $p(a - \epsilon) = -\epsilon m(a - \epsilon$ and
> $p(a + \epsilon) = \epsilon m(a + \epsilon)$ would differ in sign, contradicting the non-negativity of $p$.

This settles the case for the real roots, now for the complex roots.

> **Lemma 4** Let $p \in \mathbb{R}[x]$ and $a$ be a root. Then, $\overline{a}$ is also a root.
\
> **Proof** Observe that $\overline{p(x)} = p(\overline{x})$.

Hence, putting both lemmas together, we get
> **Corollary 5** Let $p \in \mathbb{R}[x]$ be a non-negative polynomial. Then there exists $a_1, a_2, ..., a_n \in \mathbb{C}$
such that $p(x) = \prod_{i=1}^n (x - a_i)(x - \overline{a_i})$.
>
> **Proof of Theorem 2** Note that 
> $$ p(x) = \prod_{i=1}^n (x - a_i)(x - \overline{a_i}) =  \prod_{i=1}^n (x^2 - |a_i|^2),$$
> and $(a^2 + b^2)(c^2 + d^2) = (ac-bd)^2 + (ad-bc)^2$. 

---

With this result, it is natural to ask if it generalizes. Unfortunately, [Hilbert 1888](https://doi.org/10.1007/BF01443605)
shows that there exists multivariate positive polynomials which cannot be written as a finite sum of squares. His proof was non-constructive, and we shall see a concrete counterexample here.

> **Counterexample 6** \[[Motzkin 1967](https://mathscinet.ams.org/mathscinet-getitem?mr=0223521) [^1] \]
> Let 
> $$f(x, y) = 1 - 3x^2y^2 + x^2y^4 + x^4y^2.$$
> The polynomial $f$ is non-negative, but cannot be written in the form $\sum_k (f_k(x,y))^2$ for $f_k \in \mathbb{R}[x,y].$
>
> **Exercise 7** Verify Counterexample 6 via the following steps.
>
> 1. Using the arithmetic-geometric mean $\frac{a + b + c}{3} \geq \sqrt[3]{xyz}$, show that $f$ is non-negative.
> 2. Suppose that $f(x, y) = \sum_k (f_k(x,y))^2$, then show that the degree of $f_k$ is at most 3, and that $f_k(0,y)$ and $f_k(x,0)$ are constants.
> 3. Show that $f_k(x, y) = a_k + b_kxy + c_kx^2y + d_kxy^2$ for $a_k, b_k, c_k, d_k \in \mathbb{R}$. But comparing the coefficient
of $x^2y^2$ in $f(x,y)$ and in $\sum_k (f_k(x,y))^2$ yields a contradiction.

But there are many other generalizations that are indeed true and leads to [Emil Artin's 1927](https://link.springer.com/article/10.1007%2FBF02952513) solution of Hilbert's 17-th problem and joining [the Honors Class](https://www.maa.org/press/maa-reviews/the-honors-class-hilberts-problems-and-their-solvers). 

However, that is a story for another time.

[^1]: I've have not been able to acquire the source of this article and have a look. There is a chance of circular reporting here, unfortunately.