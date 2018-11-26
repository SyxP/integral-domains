+++
title = "A Complex Step"

date = 2018-10-15

draft = true

tags = ["math", "analysis"]
summary = "Complex numbers are both useful and magical. We shall apply them in determining the derivative of real-valued fuctions."

[header]
image = ""
caption = ""
+++

"Le plus court chemin entre deux vérités dans le domaine réel passe par le domaine complexe." - Jacques Hadamard

In this blog post, we shall see more evidence of this statement. The importance of the derivative cannot be overstated, its utility arises from allowing us to analyze the behaviour of the original function. The problem we are concerned today is on finding numerical approximation to the derivative at a point.

Consider a function $f : \mathbb{R} \to \mathbb{R}$, then the derivative at $0$ is $$Df(0) = \lim_{h \to 0} \frac{f(h) - f(0)}{h}.$$

It is tempting to believe we can approximate $Df(0)$ by simply choosing a small $h \in \mathbb{R}\setminus \{0\}$, and then evaluating $\frac{f(h) - f(0)}{h}$. For a well-behaved function, this is indeed the case. 

>**Theorem 1** \[[Lagrange 1797](https://books.google.com.sg/books?id=FoM_AAAAcAAJ)\] Let $f \in C^2(\mathbb{R})$, then $$ f(h) = f(0) + Df(0)h + \frac{D^2f(\theta)}{2}h^2$$
for some $\theta \in (0, h)$.

