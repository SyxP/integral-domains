+++
title = "The Diagonal Argument"

date = 2018-03-30

draft = false

tags = ["compsci", "complexity"]
summary = "The Diagonal Argument can be used to establish the cardinality of the reals. Here, we investigate its implication in complexity theory, as well as the limitations of the method."

[header]
image = ""
caption = ""
+++

In 1891, George Cantor showed us that there are more real numbers than there are natural numbers.

>**Theorem 1** \[[Cantor 1891](http://web2.slc.qc.ca/VCarrier/Mathematics\_BNJ/Cantor\_1891.pdf) \] There is no bijection between $(0,1) \in \mathbb{R}$ and $\mathbb{N}$.
\
>**Proof** Assume the existence of a bijective function $f : \mathbb{N} \to (0,1) $, we claim that there exists $\alpha \in (0,1)$ such that $\\{ \ k \in \mathbb{N}\ \mid\  f(k) = \alpha \ \\}$ is empty. This is done via construction. Denote $g\_i(x)$ be the $i$-th digit in the decimal expansion of $x$. Let $g\_i(\alpha) = 1 + \[g\_i(f(i)) = 1\]$[^1], then for any $\ k \in \mathbb{N}$, $\alpha$ will differ from $f(k)$ in the $k$-th digit.

Today, we shall exploit the power of this argument, and to see its limitations. Chiefly, we will apply it in the context of complexity theory. As such, we shall fix our model of computation to the Multi-tape Turing Machines (MTM).

First, let us understand what exactly _is_ the diagonal argument.

We start with two sets $A \subseteq B$, and our goal is to show that this is a strict inclusion. This is shown by constructing an $\alpha$ in $B$ but not $A$. For all $\beta \in A,$ we will construct $\alpha$ in such a way that it differs (slightly) from $\beta$. This effectively is a definition, and every strict inclusion can always be proven this way. However, we'll see later when we apply it in complexity theory, it is done in a specific way called **diagonalization**.

>**Problem 2** Show that there is no bijection between any set $S$ and its power set $\mathcal{P}(S)$.

---

The next theorem we shall attack is known as the **Time Hierachy Theorem**. Intuitively, it states that when given more time, a MTM has more computing power (i.e. it can compute more functions). Let us first recall a few definitions.

A **decision problem** is a function $f : \mathbb{N} \to \\{0,1\\}$. A decision problem is **computable in** $g(X)$ **time** if there exists a MTM, on any input $X$, it will output $f(X)$ in $\mathcal{O}(g(\lceil\log{X}\rceil))$ steps. A function $f : \mathbb{N} \to \mathbb{N}$ is said to be **time-constructible** if a MTM on input $2^X$, can output $f(X)$ in $\mathcal{O}(f(X))$ steps.

>**Problem 3** Show that there exist decision problems that are not computable (i.e. there does not exist any $g$ such that it is computable in $g(X)$ time).

A complexity class is a set of decision problems. We denote $\textrm{DTIME}(f(n))$ and $\textrm{NTIME}(f(n))$ as the set of all the decision problems computable in $f(n)$ time on a deterministic and non-deterministic MTM respectively. 

>**Lemma 4 (Linear Speedup)** Let $f$ be a time-constructible function, and $c \in \mathbb{R}^+$. If a MTM computes a decision problem in $f(X)$ steps, there exists a MTM that computes the same decision problem in $cf(X) + X + 2$ steps.
\
>**Proof** See \[[Papadimitrou 2003](https://dl.acm.org/citation.cfm?id=1074233) \] page 32. 
>
>**Theorem 5 (Deterministic Time Hierarchy)** 
\
>\[[Hartmanis and Stearns 1965](http://www.ams.org/journals/tran/1965-117-00/S0002-9947-1965-0170805-7/home.html) \] Let $f, g$ be time-constructible functions, satisfying the property $f(X)\log{(f(X))} = o(g(X))$. Then, there exists a decision problem $h(X)$ not computable in $f(X)$ time but computable in $g(X)$ time. That is,
>$$\textrm{DTIME}(f(X)) \subsetneq \textrm{DTIME}(g(X))).$$
\
>**Proof** Unsurprisingly, we will use the diagonal argument to construct a decision problem $h(X)$. Let the set of MTM computing decision problems computable in $f(X)$ time be $D = \\{D\_i\\} \_ {i \in \mathbb{N}}$. 
>
> On input $X$, we will simulate $D\_X$ on input $X$ for $4f(X)$ steps. If it halts and outputs an answer, $h(X)$ will output the opposite of $D\_X(X)$, otherwise set $h(X)$ arbitrarily to $0$. By a result of [Hennie and Stearns 1966](https://dl.acm.org/citation.cfm?doid=321356.321362), the simulation can be done sufficiently efficiently, and hence $h(X) \in \textrm{DTIME}(g(X))$.
>
> If $g \in \textrm{DTIME}(f(X))$, then there exists a constant $c \in \mathbb{R}^+$ such that a MTM computes $h$ in $cf(X)$ steps. By Lemma 4, there exists a MTM $D'$ that computes $h$ in $f(X) + X + 2 \leq 4f(X)$ steps. But $D' \in D$, and by the construction of $h$, this two cannot be equal. Hence, $h(X) \notin \textrm{DTIME}(f(X))$.

Let us reflect on this flavor of the diagonal argument closely. We have constructed $h(X)$ by considering all MTM computing decision problems computable in $f(X)$ time. By simulating each machine and flipping the outcome, $h(X)$ will differ from all such decision problems. This is known as **diagonalization**. It is very important to note that this is not the same as the diagonal argument! The diagonal argument is a generic approach to prove the strict inclusion on two sets, while this uses a notion of simulation to show the strict inclusion of two complexity classes. 

Whenever we have a theorem, we should always examine its conditions. The time-constructability of $f$ is needed during the simulation, while the time-constructability of $g$ is redundant. Can we relax the condition? A result by [Borodin 1972](https://dl.acm.org/citation.cfm?id=321691) and Trakhtenbrot shows it is necessary for $f$ to be time-constructible. The other condition is that $f(X)\log{(f(X))} = o(g(X))$, and this is due to our simulation. It is not known if it is possible to simulate faster, but Problem 7 shows a strengthening in a special case.

>**Problem 6 (Nondeterministic Time Hierachy)** \[[Cook 1972](https://dl.acm.org/citation.cfm?doid=800152.804913) \] Show if $f, g$ are time-constructible functions and $f(X+1) = o(g(X))$, then
>$$\textrm{NTIME}(f(X)) \subsetneq \textrm{NTIME}(g(X)).$$
>**Problem 7 (Padding)** Let $f,g,h$ be time-constructible functions. Show that if $\textrm{DTIME}(f(X)) = \textrm{DTIME}(g(X))$, then $$\textrm{DTIME}(f(h(X))) = \textrm{DTIME}(g(h(X)).$$ 
>Fix $a\_1, a\_2, b\_1, b\_2 \in \mathbb{Q}^{\geq 0}$ with
>
>* $1 \leq a\_1 < b\_1$ or
>* $1 \leq a\_1 = b\_1$ and $a\_2 < b\_2$.
>
>Using the Padding Theorem, show $$\textrm{DTIME}(n^{a\_1}(\log{n})^{a\_2}) \subsetneq \textrm{DTIME}(n^{b\_1}(\log{n})^{b\_2}).$$
>
>**Problem 8** It is natural ask if there is any relationship between $\textrm{DTIME}$ and $\textrm{NTIME}$. Prove that for any time-constructible $f$,
>$$ \textrm{NTIME}(f(X)) \subseteq \bigcup\_{c \in \mathbb{N}}\textrm{DTIME}(c^{f(X)}).$$

Before we get depressed at the lacklustre performance of diagonalization, let us see it once more in action. Consider the generalization of the non-deterministic MTM, the **Alternating Turing Machine** (ATM). This generalization classifies all non-terminating states as $\exists$ and $\forall$ states. An internal state is accepting if

* it is an accepting terminal state,
* it is an $\exists$ state and there exists at least one configuration reachable that is an accepting terminal state,
* it is a $\forall$ state and all configurations reachable are accepting.

The **alternation coefficient** of an ATM is the number of times an ATM goes from an $\exists$ state to a $\forall$ state or vice versa. The complexity class $\exists\textrm{TIME}(g(X), k)$ (or $\forall \textrm{TIME}(g(X), k)$) is the set of all decision problems $f(X)$ computable on an ATM with alternation coefficient $k$ using $\mathcal{O}(g(\lceil\log{X}\rceil))$ steps and the initial state being an $\exists$ state (or $\forall$ state respectively).

For the rest of this article, set $\textrm{P} = \cup\_{c \in \mathbb{N}} \textrm{DTIME}(X^c)$ and $\textrm{NP} = \cup\_{c \in \mathbb{N}} \textrm{NTIME}(X^c)$.

>**Problem 9** Verify $\textrm{NP} = \bigcup\_{c \in \mathbb{N}}\exists\textrm{TIME}(X^c, 0)$.
>
>**Problem 10 (No Complementary Speedup)** 
\
> \[[Chandra and Stockmeyer 1976](http://ieeexplore.ieee.org/document/4567893/) \] Show via diagonalization that for all time-constructible $f(X)$ and $k \in \mathbb{N}$,
>$$\exists\textrm{TIME}(f(X), k) \nsubseteq \forall\textrm{TIME}(o(f(X)), k).$$

---

In light of our previous successes, we might attempt to attack the separation of other complexity classes. One of the central problem in complexity theory is to determine whether $\textrm{P}$ and $\textrm{NP}$ are equal. This problem cannot be solved via the diagonalization. By studying the mode of failure, we can understand the limitations of diagonalization, the failure to overcome the **relativization barrier**, and gain a deeper understanding of the approach.

We can augment a MTM with an additional tape which we shall term as the **oracle tape** and a fixed decision problem $f$. In one step, the MTM may alternatively query the value of $f(X)$ where $X$ is the contents of the Oracle tape. A decision problem $g$ solvable by the augmented MTM is defined to be in the complexity class $A^B$ where $A$ is a complexity class containing this MTM ignoring the augmentation, an $B$ is some complexity class containing $f$.

Note that not all complexity classes admit an oracle, as it relies on the notion of some MTM computing the decision problems in the class. We shall define **structural** complexity classes as classes which do admit an oracle. By nature of their definition, $\textrm{DTIME}$, $\textrm{NTIME}$, $\exists\textrm{TIME}$ and $\forall\textrm{TIME}$ are structural.

We never formally defined diagonalization, only giving it a sketch. In some sense, it is due to the diversity of the situations where it is applicable such as Theorem 5, Problem 6 and Problem 10. Thus, the next statement can only remain an observation.

>**Observation 11** Let $A,B$ be structural complexity classes. If diagonalization shows $A \neq B$, then for all complexity classes $C$, diagonalization shows $A^C \neq B^C$.
\
>**Evidence** This can be seen from how the simulation is "oracle-agnostic", and doesn't know the presence of an oracle at any step. Thus, diagonalization should still work when both machines are given oracle access.

Observation 11 gives us a barrier to the technique. If for two structural complexity classes $A$ and $B$, there exist complexity classes $C, D$ such that $A^C = B^C$ and $A^D \neq B^D$, then diagonalization can never help us determine which is the case. As aforementioned, this is the case for the central problem $\textrm{P} \stackrel{?}{=} \textrm{NP}$:

>**Theorem 12** \[[Baker, Gill and Solovay 1975](https://epubs.siam.org/doi/abs/10.1137/0204037) \] There exist complexity classes $A$, $B$ such that $\textrm{P}^A = \textrm{NP}^A$ and $\textrm{P}^B \neq \textrm{NP}^B$.
\
>**Proof** This is done by constructing complexity classes $A$ and $B$.
\
>Consider the complexity class $\textrm{EXP} = \bigcup\_{c \in \mathbb{N}} \textrm{DTIME}(2^{n^c})$. It is evident that $\textrm{EXP} \subseteq \textrm{P}^\textrm{EXP} \subseteq \textrm{NP}^\textrm{EXP}$. By Problem 8, $\textrm{NP} \subseteq \textrm{EXP}$ and thus $\textrm{NP}^\textrm{EXP} \subseteq \textrm{EXP}^\textrm{EXP} = \textrm{EXP}$.
>
>For all decision problems $B$, we can construct the decision problem $U\_B$ setting $U\_B(x) = [\exists y$ such that $\log(x) = \lceil\log(y)\rceil$ and $B(y) = 1]$.  Then, $U\_B \in \textrm{NP}^{\\{B\\}}$ as it can non-deterministically guess an $x$ with said properties. It now suffices to construct $B$ such that $U\_B \notin \textrm{P}^{\\{B\\}}$. Once again, we proceed by diagonalization(!) Hence, we order $\textrm{P} = \\{M\_i\\} \_ {i \in \mathbb{N}}$.
>
>We proceed in stages, at stage $i$, we would like to construct $B\_i$ such that $U\_{B\_i}$ would not be answered correctly by the first $i$ decision problems with $B\_i$ as an oracle and that $B\_j \subseteq B\_i$ for all $0 \leq j < i$. For notation convenience, set $B\_{-1} = \varnothing$ and $S(i,j,k)$ be the MTM $M\_i$ with oracle $B\_j$ and input $2^k$
>
>For each $i$ choose the smallest $n\_i$ such that for all $0 \leq j < i$, no $S(j,i-1,n\_j)$ queries any string $x$ with $n\_i = \lceil\log(x)\rceil$ and $n\_j < n\_i$. Moreover, $S(i,i-1,n\_i)$ should not make more than $2^{n\_i}$ queries to the oracle. This is assured as $M\_i$ can only make polynomially many queries. 
>
>Each time $S(i,i-1,n\_i)$  makes a query that has not been previously made in any of the previous stages, the oracle will return 0 (If it has been made, it must answer consistently). This ensures that $B\_{i-1}$ contains no string $x$ with $n\_i = \lceil\log(x)\rceil$. If $S(i,i-1,n\_i) = 1$, setting $B\_i = B\_{i-1}$ suffices. Otherwise, we choose some string $y$ with $n\_i = \lceil\log(y)\rceil$ that has not been queried, then setting $B\_i = \\{y\\} = B\_{i-1}$. In either case, $S(i,i,n\_i)$ will answer wrongly.
>
>Finally, set $B = \bigcup\_{i \in \mathbb{N}} B\_i$. 

Naturally, we would like to know what other classes would have the relativization barrier. In the above paper, Meyer asks the following problems.

>For the following problems, we define $\exists\_k\textrm{P} = \bigcup\_{c \in \mathbb{N}} \exists\textrm{TIME}(X^c, k)$ and $\forall\_k\textrm{P}= \bigcup\_{c \in \mathbb{N}} \forall\textrm{TIME}(X^c, k)$. 
>
>**Problem 13** \[[Baker and Selman 1979](https://www.sciencedirect.com/science/article/pii/0304397579900434) \] Show there exist complexity classes $A$,  $B$ such that $\exists\_1\textrm{P}^A = \forall\_1\textrm{P}^A$ and $\exists\_1\textrm{P}^B \neq \forall\_1\textrm{P}^B$.
>
>**Problem 14** \[[Yao 1985](https://dl.acm.org/citation.cfm?id=1382893) \]  Prove for all $k \geq 2$, there exist complexity classes $A, B$ such that $\exists\_k\textrm{P}^A = \forall\_k\textrm{P}^A$ and $\exists\_k\textrm{P}^B \neq \forall\_k\textrm{P}^B$.

[^1]: This is the **Iverson Bracket** notation, $\[P\]$, which evaluates to 1 when $P$ is true, 0 otherwise.
