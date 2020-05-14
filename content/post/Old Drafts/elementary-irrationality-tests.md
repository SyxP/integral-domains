+++
title = "Elementary Irrationality Tests"

date = 2018-04-27

draft = true

tags = ["math", "number theory", "primes", "analysis", "algebra"]
summary = ""

[header]
image = ""
caption = ""
+++

$ %Header LaTeX
\newcommand{\Engel}\[2\]{ \mathcal{E}\left \[\frac{#1}{#2}\right \] }
\newcommand{\prt}\[2\]{\sqrt\[\leftroot{-3}\uproot{3}#1\]{#2}}
\newcommand{\dlim}\[1\]{\lim\_{#1\to\infty}}
\newcommand{\decp}\[1\]{\mathcal{D}(#1)}
$Apocryphally, Hippasus was drowned at sea, for divulging god's secret of the irrationality of $\sqrt{2}$. The irrationality of $\sqrt{2}$ is one of the oldest theorems in mathematics and undoubtably, every student will know at least one proof. The following is classic.

>**Theorem 1** $\sqrt{2}$ is irrational.
>**Proof** Suppose not, then $\sqrt{2} = \frac{a}{b}$ for some integers $a$ and $b$ with $\gcd(a,b) = 1$. Rearranging yields $2b^2 = a^2$, which implies that $a$ is even, and we can write $a = 2c$ for some integer $c$. But then $2b^2 = (2c)^2$ and $b^2 = 2c^2$, thus $b$ is even, contradicting $\gcd(a,b) = 1$.

The above is a proof by contradiction at its barest. Allow me to indulge in the following quote of G. H. Hardy, "\[A proof by contradiction\] is one of a mathematician's finest weapons. It is a far finer gambit than any chess play: a chess player may offer the sacrifice of a pawn or even a piece, but a mathematician offers the game."

Naturally, we ask for generalizations.

>**Problem 2** Show that for any integer $k \geq 2$, and $k$ is not a perfect square, $\sqrt{k} \notin \mathbb{Q}$.
>**Problem 3** Determine all integers $a, b \geq 2$ such that $\log\_a(b) \notin \mathbb{Q}$. (You might require the **Fundamental Theorem of Arithmetic**: Every integer greater than 1 can be represented as a product of primes, moreover the product is unique up to reordering the terms.)

Today, let us play around with elementary techniques to show various numbers are irrational.

---

Another well-known irrational number with an elementary proof is the mathematical constant $e$. The first known proof of this was due to [Euler 1737](http://eulerarchive.maa.org/pages/E071.html) using continued fractions. This too is a beautiful technique, but will not be covered today (but perhaps in a future blog?) Here, we will recreate the proof by Fourier.


Let us denote the **decimal part** of a number $x$ as $\decp{x}$. Our strategy to show numbers are irrational is the **irrationality criterion**: For any $q \notin \mathbb{Q}^+$, if for any $\epsilon > 0$, there exist $N \in \mathbb{N}$ such that $0 < \decp{Nq} < \epsilon$.

>**Theorem 4** \[Fourier 1815\] $e$ is irrational.
>**Proof** Observe that for any $B$, $$\decp{B!e} = \decp{B!\sum\_{k=0}^\infty\frac{1}{k!}} = \decp{\sum\_{k=B+1}^\infty\frac{B!}{k!}}.$$ But the last series is nonzero and $$\sum\_{k=B+1}^\infty\frac{B!}{k!} \leq \sum\_{c=1}^\infty \frac{1}{(B+1)^c} = \frac{1}{B}.$$ As $B$ was arbitrary, by the irrationality criterion, $e$ is irrational.

Define **generalized Engel Summation** as $\Engel{b\_n}{a\_n} = \sum\_{i=1}^\infty \frac{b\_1b\_2...b\_i}{a\_1a\_2...a\_i}$. We would generalize the results in Theorem 4 to generalized Engel Summations by essentially the same proof.

>**Theorem 5** Let $\\{b\_i\\}$ and $\\{a\_i\\}$ be nonzero integer sequences. If there exist $k, N\_0$ such that $|b\_n| \leq k$ is bounded and $a\_n \geq k^2n$ for all $n > N\_0$, then the generalized Engel summation $S = \Engel{b\_n}{a\_n}$ exists and is irrational.
>
>**Proof** Denote $\kappa\_n = (a\_1a\_2...a\_n)$ and $\gamma\_n = (b\_1b\_2...b\_n)$. Moreover, as $\decp{\kappa\_m \Engel{b\_n}{a\_n}} = \decp{\gamma\_m \Engel{b\_{m+n}}{a\_{m+n}}}$, without loss of generality, set $N\_0 = 0$.
>
>First we show the existence. For any function $f$ with $\dlim{n} f(n) = 0$, we have that $\dlim{n} \prod\_{i=1}^n f(n) = 0$. Hence, $\dlim{n} \prt{n}{\left |\frac{\gamma\_n}{\kappa\_n}\right |} = 0$. By the root test, $S$ converges absolutely.
>
>Consider $S' = \decp{|\kappa\_{m} S|}$. First, we have $S'$ is bounded, $$S' \leq |\gamma\_{m}| \Engel{k}{a\_{m+n}} \leq k^{m}\left (\frac{e^{1/k}}{k^{2m}(m+1)}\right ),$$ where the last inequality is due to Taylor's Theorem. Moreover, we have $$S' \geq \frac{|\gamma\_mb\_{m+1}|}{a\_{m+1}}\left (1 - \Engel{k}{a\_{m+n+1}}\right ) \geq frac{|\gamma\_mb\_{m+1}|}{a\_{m+1}}\left (1 - 

<!---
Discuss assumptions. Sylvester Sequence.
The assumption is necessary as $\Engel{1}{k} = \frac{1}{k-1}$.
-->
This result is immediately useful.

>**Corollary 6** $\pi$ is irrational.
>**Proof** For all $a,b \in \mathbb{Z}$, $a \neq 0$, we will have that $\cos(\frac{a}{b})$ is irrational. This follows from $$\cos(\frac{a}{b}) = 1 + \Engel{-a^2}{b^2(2n)(2n-1)},$$ by Theorem 5, this is irrational. But $\cos(\pi) = -1$ is rational. Hence, $\pi$ is irrational.

>**Problem 8** Show that the converse of the irrationality criterion holds. For all $k \notin \mathbb{Q}^+$ and real $\epsilon > 0$, there exists $N \in \mathbb{N}$ such that $0 < \\{Nk\\} < \epsilon$.

---
**Acknowledgments**

The material here is based partially on [Loya's Amazing and Aesthetic Aspects of Analysis](https://www.amazon.com/Amazing-Aesthetic-Analysis-Undergraduate-Mathematics/dp/1493967932) and [Riasat's blog post](https://sriasat.wordpress.com/2013/03/19/an-irrationality-criterion/).
