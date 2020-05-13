+++
title = "Dirichlet's Theorem"

date = 2020-05-13

draft = false

tags = ["math", "number theory", "primes", "complex analysis", "algebra"]
summary = ""

[header]
image = ""
caption = ""
+++

Every integer has a prime decomposition. Thus, to study the integers, we study the primes. It is not surprising that one of the oldest fields of mathematics is to understand the properties of the primes.

>**Theorem 1** \[ Euclid c. 300 BC \] There are infinitely many primes.
\
>**Proof** Let  $S(a,b)$ be the set $\\{an + b \in \mathbb{N} \mid an + b \text{ is prime}\\}$ and $f(N) = 2N + 1$, we shall show that $S(2,1)$ is an infinite set. 
>
>Assume $S(2,1)$ is a finite set. Consider a prime factor $F$ of $M = f(\prod\_{p \in S(2,1)} p)$. Since $F$ must be of the form $2k + 1$, $F \in S(2,1)$. Hence, $M \equiv 1 \ (\mathrm{mod}\ F)$.
>
>This is a contradiction, so $S(2,1)$ cannot be a finite set.

The above proof compels the question on the finiteness of $S(a,b)$ for $a,b \in \mathbb{N}$. When $a,b$ aren't coprime, $|S(a,b)| \leq 1$.  But what if $a,b$ are coprime? We can tackle a few special cases:

>**Problem 2** Augment the above proof to show that $S(4,3)$ and $S(6,5)$ are infinite.
\
>**Problem 3** Show that if $N^2 + 1 \equiv 0 \ (\mathrm{mod}\ p)$ for some prime $p$, then $p \equiv 1 \ (\mathrm{mod}\ 4)$. Hence, by considering $f(N) = N^2 + 1$, show $S(4,1)$ is infinite.
>Note: This is saying when $p \equiv 3 \ (\mathrm{mod}\ 4)$, $-1$ is a quadratic non-residue modulo $p$. Moreover, if $p \equiv  5\ (\mathrm{mod}\ 6)$, $-3$ is a quadratic non-residue modulo $p$. So, we can contemplate setting $f(N) = 4N^2 + 3$ to show $S(6,1)$ is infinite.
\
>**Problem 4** For any $n \in \mathbb{N}$, let $U\_n$ be the set of $n$-th primitive roots of unity. Denote the **cyclotomic polynomials** as $\Phi\_n(x) = \prod\_{\eta \in U\_n} (x - \eta)$. Show that if a prime $p$ divides $\Phi\_M(k)$ for some $k, M \in \mathbb{N}$, either $p \equiv 1\ (\mathrm{mod}\ M)$ or $p$ divides $2M$. 
>Hence, by considering $f(N) = (2M)!\cdot\Phi\_M(N) + 1$, show $S(M,1)$ is infinite for all $M$.
\
>**Problem 5** Find another nontrivial pair $(a,b) \in \mathbb{N}^2$ where $S(a,b)$ is infinite.


Indeed, it is true that if $a,b$ are coprime, $S(a,b)$ is infinite. This is known as **Dirichlet's Theorem** and we'll prove it today. It may be tempting to generalize Euclid's proof, and we had moderate success out of it (see [Murty and Thain 2006](https://projecteuclid.org/euclid.facm/1229442627) for more examples). But as Problems 2 through 5 shows, the arguments may get increasingly ad hoc. We shall instead start by playing around with a different proof of Theorem 1.
Furthermore, it might not even be possible, see a blurb by [Conrad](https://kconrad.math.uconn.edu/blurbs/gradnumthy/dirichleteuclid.pdf) on an earlier result of Murty.

---

In Euler footsteps, we shall start by studying the **zeta function** $\zeta(\sigma)$. It is the analytic continuation[^1] of $\sum\_{k \in \mathbb{Z}^+} k^{-\sigma}$ defined on $\Re(\sigma) > 1$. In Problem 7, we shall see that the series converges when $\Re(\sigma) > 1$. The relationship of $\zeta(\sigma)$ and the primes is illuminated by the following theorem:

>**Theorem 6** \[[Euler 1744](http://eulerarchive.maa.org/pages/E072.html) \] For all $\Re(\sigma) > 1$, 
>$$\zeta(\sigma) = \prod\_{p \text{ prime}} \frac{1}{1 - p^{-\sigma}}.$$
\
>**Problem 7** We shall sketch the proof of Theorem 6. Reconstruct the proof.
> Let $\sigma \in \mathbb{C}$ with $\Re(\sigma) > 1$ and $\mathbb{P}\_N$ be the set of primes $\leq N$.
> 1. As $|\sum\_{k = M+1}^N k^{-\sigma}| \leq \int\_M^N x^{-\Re(\sigma)} \mathrm{d}{x}$, $\zeta(\sigma)$ converges absolutely. 
> 2. For all $N \in \mathbb{Z}^+$, $\prod\_{p \in \mathbb{P}\_N} (1 - p^{-\sigma})^{-1} = \sum\_{k=1}^N k^{-\sigma} + \sum\_{k \in I} k^{-\sigma}$, where $I$ is some subset of $ \mathbb{Z}^+ \setminus \\{1,2,...,N\\}$. As $N$ tends to $\infty$, the expression on the right converges to $\zeta(\sigma)$ and the expression on the left is definitionally $\prod\_{p \text{ prime}} (1 - p^{-\sigma})^{-1}$.

This leads to an alternate proof of Theorem 1.

>**Corollary 8** There are infinitely many primes.
\
>**Proof** If there were finitely many primes, $\lim\_{\sigma \rightarrow 1} \prod\_{p \text{ prime}} (1 - p^{-\sigma})^{-1}$ would converge. But $\lim\_{\sigma \to 1} \zeta(\sigma) $ diverges.

An equivalent way to think about Corollary 8 is:

$$\begin{aligned}
\log(\zeta(\sigma)) &= \sum\_{p \text{ prime}} \log(\frac{1}{1 - p^{-\sigma}}) = \sum\_{p \text{ prime}} \sum\_{k=1}^\infty \frac{p^{-k\sigma}}{k} \\\\
&= \sum\_{p \text{ prime}}\frac{1}{p^\sigma} + \sum\_{p \text{ prime}}\sum\_{k=2}^\infty \frac{p^{-k\sigma}}{k}
\end{aligned}$$

for some $\sigma \in \mathbb{C}$ with $\Re(\sigma) > 1$. The sum $\sum\_{p \text{ prime}}\sum\_{k=2}^\infty k^{-1}p^{-k\sigma}$ is bounded above by $C + \sum\_{p = 2}^\infty\sum\_{k=N}^\infty k^{-2}p^{-2}$ for some $C, N \in \mathbb{N}$. Thus, Corollary 8 can be stated as the statement, $\lim\_{\sigma \to 1} \sum\_{p \text{ prime}} p^{-\sigma}$ diverges.

{{% alert warning %}}
We have to be a little careful, as $\log$ is not necessarily well-defined over the complex numbers.  Fortunately, we are taking
logarithms of products with each term of the form $(1 - \alpha)^{-1}$ with $|\alpha| < 1$ when $\Re{\sigma} > 1$. Hence, we can take $\log (1 - \alpha)^{-1} = \sum_{k = 1}^\infty \frac{\alpha^k}{k}$.
{{% /alert %}}

Inevitably, we would like to understand the power of our approach. It is very seductive to consider $\prod\_{p \in S(a,b)} (1 - p^{-\sigma})^{-1}$ or $\sum\_{p \in S(a,b)} p^{-\sigma}$. If either diverges as $\sigma$ tends to $1$, we would have shown that $S(a,b)$ is infinite. However, our way to proceed is not obvious, as the product of two numbers of the form  $b\ (\mathrm{mod}\ a)$ have little reason to be of the form $b\ (\mathrm{mod}\ a)$, the product $\prod\_{p \in S(a,b)} (1 - p^{-\sigma})^{-1}$ may bear little resemblance to the sum $\sum\_{k=1}^\infty (ak + b)^{-\sigma}$.

As in life, there are no coincidences in mathematics. The failure of our methods is because the characteristic function $Ch(k) = \[k \equiv b\ (\mathrm{mod}\ a)\]$[^2] is not a multiplicative function. A **multiplicative function** is defined as a function  $\pi : \mathbb{Z}^+ \to \mathbb{C}$ with the properties $\pi(1) = 1$ and $\pi(ab) = \pi(a)\pi(b)$ for all $a,b \in \mathbb{Z}^+$.[^3] To completely understand why the lack of multiplicativity is a problem, observe the following generalization of Theorem 6.

> Let $\pi$ be a multiplicative function bounded above on $\mathbb{Z}^+$. 
\
>**Theorem 9**  For all $\Re(\sigma) > 1$, $$\sum\_{k=1}^\infty \frac{\pi(k)}{k^\sigma} = \prod\_{p \text{ prime}} (1 - \frac{\pi(p)}{p^\sigma})^{-1}.$$
\
> **Problem 10** As is routine, prove Theorem 9. Hence, explain the above-mentioned failure.
\
> **Problem 11** We define the **Dirichlet L-function**, $L(\sigma,\pi) = \sum\_{k=1}^\infty \pi(k)k^{-\sigma}$ like the left hand side of Theorem 9. Show for all $\Re(\sigma) > 1$, there exists a constant $C \in \mathbb{C}$ such that $$\log(L(\sigma,\pi)) = \sum\_{p \text{ prime}} \frac{\pi(p)}{p^\sigma} + C.$$

Dirichlet's beautiful, key insight is that it is possible to decompose our non-multiplicative characteristic function $Ch(k)$ into multiplicative ones. In order to construct these multiplicative functions, we shall explore a little representation theory.

---

The following is the most unmotivated step in this proof, mainly because we omit the discussion of representations. The rationale is twofold. First, to derive the necessary results in a complete discussion would be too long and beyond the scope of this blog post. Secondly, the author hopes that the result would serve as a motivation in itself, giving an application of the viewpoints pioneered by representation theory.

A **Dirichlet character** modulo $a$ is a group homorphism from $(\mathbb{Z}/a\mathbb{Z})^\times$ to $\mathbb{C}^\times$. We shall denote the set of Dirichlet characters modulo $a$ as $\chi\_a$. Moreover, it is convenient to associate each Dirichlet character $\chi \in \chi\_a$ to a multiplicative function by setting $\chi(N)$ to $0$ when $\gcd(N,a) \neq 1$.

>**Theorem 12** The set of Dirichlet characters modulo $a$, $\chi\_a$, has a group structure under pointwise multiplication. Additionally, the size $|\chi\_a| = |(\mathbb{Z}/a\mathbb{Z})^\times| = \phi(a)$ where $\phi$ is the Euler totient function.
\
>**Proof** The trivial group homomorphism is in $\chi\_a$ and serves as our identity. Associativity may be checked and the existence of inverse follows from complex conjugation in $\mathbb{C}^\times$. Furthermore, $\chi\_a$ inherits commutativity from $\mathbb{C}^\times$.
>Pick a non-trivial element $e \in (\mathbb{Z}/a\mathbb{Z})^\times$ and write $\langle e \rangle$ as the (cyclic) group generated by $e$. For a Dirichlet character $\chi$, we can pick $\chi(e)$ to be an arbitrary $|\langle e \rangle|$-th root of unity. Repeating the argument recursively on $(\mathbb{Z}/a\mathbb{Z})^\times/\langle e \rangle$, we get $|\chi\_a| = |(\mathbb{Z}/a\mathbb{Z})^\times|$.

In general, there is a notion of "orthogonality" of characters. Here, we can view it as a way to reconstruct our characteristic function. To simplify notation, we shall fix $a, b \in \mathbb{Z}^+$ with $a$ and $b$ coprime. Moreover, we will write $b'$ to denote the inverse of $b$ in the group $(\mathbb{Z}/a\mathbb{Z})^\times$.

>**Theorem 13** For $n \in \mathbb{Z}^+$, $$\sum\_{\chi \in \chi\_a} \overline{\chi(b)}\chi(n) = \phi(a)\cdot\[n \equiv b\ (\mathrm{mod}\ a)].$$
\
>**Proof** There are three cases to consider:
>1. If $\gcd(n,a) \neq 1$, $\chi(n) = 0$ for all $\chi$. In this case, the sum is 0.
>2. If $n \equiv b\ (\mathrm{mod}\ a)$, $\overline{\chi(b)}\chi(n) = \overline{\chi(b)}\chi(b) = 1$ for all $\chi$. In this case, the sum is the order of $\chi\_a$, which is $\phi(a)$ by Theorem 12.
>3. The remaining case occurs when $\gcd(n,a) = 1$ but $n \not\equiv b\ (\mathrm{mod}\ a)$. In which case, we can pick a $\Psi \in \chi\_a$ with $\Psi(b'n) \neq 1$. Then, $$\Psi(b'n)\sum\_{\chi \in \chi\_a} \overline{\chi(b)}\chi(n) = \sum\_{\chi \in \chi\_a} (\Psi\chi)(b'n) = \sum\_{\chi \in \chi\_a} \chi(b'n).$$ As $\Psi(b'n) \neq 1$, $\sum\_{\chi \in \chi\_a} \overline{\chi(b)}\chi(n) = 0$. 
>
>**Corollary 14** For all $\Re(\sigma) > 1$, there exists a constant $C \in \mathbb{C}$, $$\sum\_{p \in S(a,b)} p^{-\sigma} = \frac{1}{\phi(a)}\sum\_{\chi \in \chi\_a} \overline{\chi(b)} \log(L(\sigma,\chi)) + C.$$
\
>**Proof** Apply Theorem 13 and Problem 11 to $\sum\_{p\in S(a,b)} Ch(p) p^{-\sigma}$.

Recall that we wish to show $\sum\_{p \in S(a,b)} p^{-\sigma}$ diverges as $\sigma$ tends to 1, it now suffices to show the overall contributions of  $\log(L(\sigma,\chi))$ diverges instead. 

Let's begin by computing the contribution of the trivial group homomorphism $\chi\_0(k)$. 

By Theorem 9, $L(\sigma,\chi\_0) = \prod\_{p \text{ prime}} (1 - \chi\_0(p)p^{-\sigma})^{-1}$, which must diverge as $\sigma$ tend to 1 because there are only finitely many primes not coprime to $a$. As this contribution diverges, we are left with showing that $L(1,\chi)$ is non-zero for non-trivial $\chi$. (This quantity is bounded above by $\zeta(\sigma)$, hence convergent.)

The following approach is by [Serre 1973](http://www.springer.com/gp/book/9780387900407). We shall 
merely sketch the proof here and I refer you to study Serre's excellent text (Chapter VI) carefully for the details. 

> **Theorem 15** If $\chi$ is non-trivial, $L(1, \chi)$ is non-zero.
\
>**Sketch of a Proof** 
>
>1. The zeta function $\zeta(s)$ is meromorphic on $\Re(s) > 0$ with a simple pole at $s = 1$, and holomorphic away from $s = 1$.
Hence, $L(\sigma, 1)$ has a simple pole when $\sigma = 1$ and holomorphic away from $\sigma = 1$ on
$\Re(\sigma) > 0$ because
$L(s,1)$ is "in essence" equal to $\zeta(s)$ except for finitely many terms, and thus
share similar behaviour.
>2. For any **Dirichlet series**, a series of the form $D(s) = \sum_k \frac{a_k}{k^s}$,
when $a_k$ is bounded, $D(s)$ converges absolutely on $\Re(s) > 1$ and when $\sum_{k = m}^n a_k$
is bounded for all $m, n$, $D(s)$ converges on $\Re(s) > 0$.
>3. Consider the function $\zeta\_\alpha (\sigma) =  \prod\_{\chi \in \chi\_a} L(\sigma,\chi)$. By
the second step, $L(\sigma, \chi)$ is finite for all $\Re(\sigma) > 0$ and $\chi$ non-trivial. Hence, the product
$\zeta_\alpha(\sigma)$ is meromorphic on $\Re(\sigma) > 0$ with at most a simple pole at $\sigma = 1.$
>4. If we have that $L(1, \chi)$ is zero for some non-trivial $\chi$, then $\zeta\_\alpha$ will be
analytic on $\Re(\sigma) > 0.$
>5. When $p \nmid \alpha$, let $|p|$ denote the order of $p$ in $(\mathbb{Z}/\alpha\mathbb{Z})^\times$. Then,
we get the product $\prod\_{\chi \in \chi\_a}(1 - \chi(p)n) = (1 - n^{|p|})^{-\phi(\alpha)/|p|}.$ Thus,
>$$\zeta\_\alpha(\sigma) = \prod_{p \nmid \alpha} \left( 1 - p^{|p|\sigma} \right)^{-\phi(\alpha)/|p|}.$$
>6. Finally, as $|( 1 - p^{-|p|\sigma})^{-\phi(\alpha)/|p|}| \geq |(1 - p^{-\phi(\alpha)\sigma})^{-1}|$, we
have that $\zeta\_\alpha(\sigma)$ as a Dirichlet series has all its coefficients greater than or equal to
$\sum_{k, \alpha \text{ coprime},\\ k = 1}^\infty k^{-\phi(\alpha)\sigma}$ but the latter summation diverges as $\sigma \to \frac{1}{\phi(\alpha)}$, which contradicts the analyticity in Step 4.  

Wow. That has been a rather technical ride, and perhaps the heart of the content and difficulty of Dirichlet's Theorem. (The author does confess that he is cheating by not rigorously filling in the details of the hardest part of the proof. It also took two years, since he started writing this blog post, and a course in Complex Analysis to finally understand the proof.)

This leaves us with a few questions.

1. Why do we need all this machinery and what does the zeta function illuminate about the primes?
This is a fairly deep question and perhaps requires
a careful study of analytic number theory. 
2. Can we avoid this machinery? Probably, see an "almost" proof by [Erdös](https://kam.mff.cuni.cz/~klazar/ln_antcII.pdf)...

---
**Acknowledgements**

There have been various sources I referenced in the process of writing this blog post, namely, [Serre's A Course in Arithmetic](http://www.springer.com/gp/book/9780387900407), [Linear Representations of Finite Groups](http://www.springer.com/gp/book/9780387901909), [Overholt's A Course in Number Theory](https://bookstore.ams.org/gsm-160) and [Kowalski's An Introduction to the Representation Theory of Groups](https://bookstore.ams.org/gsm-155). Moreover, I also consulted [Tran's notes](https://sites.math.washington.edu/~morrow/336_14/papers/austin.pdf) and [Mathew's blog](https://amathew.wordpress.com/2010/06/02/dirichlets-theorem-on-primes-in-arithmetic-progressions-digression/).

[^1]: An **analytic continuation** of a complex function $f$ defined on a non-empty open set $U \in \mathbb{C}$ is an analytic function $g$ such that $f(x) = g(x)$ for each $x \in U$. The finer details of analytic continuations are not required in this proof.

[^2]: This is the **Iverson Bracket** notation, $\[P\]$, which evaluates to 1 when $P$ is true, 0 otherwise. 

[^3]: Note that this property is sometimes called **completely multiplicative**.
