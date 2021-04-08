---
title: Lagrange multipliers and constrained optimization
comments: 9
---

{% include post-header.md %}

(01 Feb 2021) Reiterating perhaps the main point of my website, I hope to organize the many small things that I learn as I go along so that they are easily accessible for future reference. With that in mind, this post will be quite short, and mostly follow these [MIT OCW Notes](https://ocw.mit.edu/courses/mathematics/18-02sc-multivariable-calculus-fall-2010/2.-partial-derivatives/part-c-lagrange-multipliers-and-constrained-differentials/session-40-proof-of-lagrange-multipliers/MIT18_02SC_notes_22.pdf) with some of my own details filled in.


**Lemma**: The gradient of a function $f$ is perpendicular to the level sets of $f$.

*Proof*: Consider a curve parametrized by $t$, so that $\vec\gamma(t) = (x_1(t),\dots, x_n(t))$. We say that $\gamma$ is a level curve if

$$f\parentheses{x_1(t),\dots,x_n(t)} = c$$

for all $t$ and some constant $c$ independent of $t$. Then

$$\begin{aligned}
0 &= \frac{d}{dt}f\parentheses{x_1(t),\dots, x_n(t)}\\
&= \vec\nabla f \cdot \frac{d}{dt}\vec \gamma.
\end{aligned}$$

To say that the level curve is perpendicular to the gradient is precicely to say that $\frac{d}{dt}\vec \gamma$ is perpendicular to $\vec \nabla f$, which we've indeed just shown by showing that the dot product is zero. Since this is true for all level curves $\vec \gamma$, it is true in general for the level sets. {% include endproof.html %}


**Theorem**: Let $(x_1^\ast,\dots, x_n^\ast)$ denote the location of a local maximum value of $f(x_1, \dots,x_n)$ constrained to the set of points defined by $g(x_1, \dots, x_n) = 0$. Then $\parentheses{\vec \nabla f}\big\rvert_{(x_1^\ast, \dots,x_n^\ast)} \propto \parentheses{\vec \nabla g}\big\rvert_{(x_1^\ast, \dots,x_n^\ast)}$.

*Proof*: Let $\vec\gamma(t) \coloneqq (x_1(t),\dots, x_n(t))$ denote a curve such that $\vec\gamma(0) = (x_1^\ast,\dots, x_n^\ast)$ and $\vec \gamma(t)$ lies on the constraint set (i.e. the set defined by $g(x_1,\dots, x_n) = 0$) for all $t$. Let $h(t) \coloneqq f(x_1(t),\dots, x_n(t))$, so that $h(0)$ is a local maximum of $f$. Then

$$\frac{dh}{dt}\bigg\rvert_{t=0} = 0$$

since $t=0$ is a local maximum. Using the chain rule,

$$0 = \parentheses{\vec \nabla f \cdot \frac{d}{dt}\vec\gamma}\bigg\rvert_{t=0}.$$

Since $\vec \gamma(t)$ is any curve that lies on the constraint set (provided that $\vec \gamma(0) = (x_1^\ast,\dots, x_n^\ast)$), the gradient of $f$ at the local maximum must be perpendicular to the whole constraint set. By the Lemma, we also know that $\parentheses{\vec \nabla g}\big\rvert_{(x_1^\ast,\dots, x_n^\ast)}$ is perpendicular to the constraint set, since the constraint set is precisely a level set of $g$.

$g(x_1, \dots, x_n)=0$ defines an $n-1$ dimensional surface. Thus, if two $n$ dimensional vectors are perpendicular to it at a point, then there is only one other dimension that they can be oriented. Therefore, the two vectors must be parallel at that point. So we can conclude that $\parentheses{\vec \nabla f}\big\rvert_{(x_1^\ast,\dots, x_n^\ast)}$ is parallel to $\parentheses{\vec \nabla g}\big\rvert_{(x_1^\ast,\dots, x_n^\ast)}$, proving the theorem. {% include endproof.html %}


**Corollary**: The local maximum of a function $f(x_1, \dots. x_n)$ subject to the constraints that $g_i(x_1, \dots, x_n) = 0$ for $i=1,\dots,\ell$ satisfies $\vec\nabla L = 0$, where

$$L(x_1, \dots, x_n, \lambda_1, \dots, \lambda_\ell) = f(x_1, \dots, x_n) - \sum_{i=1}^\ell \lambda_i g_i(x_1, \dots, x_n),$$

and

$$\vec \nabla = \parentheses{\frac{\partial}{\partial x_1}, \dots, \frac{\partial}{\partial x_n}, \frac{\partial}{\partial \lambda_1}, \dots, \frac{\partial}{\partial \lambda_\ell}}.$$

The $\lambda_i$ are called *Lagrange multipliers*, and $L$ is called the *Lagrangian*.


### Example: Exponential distribution

Suppose we know the mean $\mu$ of a probability distribution $p(x)$ on $x \in [0,\infty)$, but nothing else. Then the best assumption about the distribution that we can make is that it maximizes the entropy, subject to a fixed mean. So we must maximize

$$L = -\int dx~~ p(x) \ln p(x) - \lambda_1 \parentheses{\int dx~~ p(x) - 1} - \lambda_2 \parentheses{\int dx~~ xp(x) - \mu}.$$

Then we have that

$$\begin{aligned}
0 &= \frac{\partial L}{\partial p}\\
&= \int dx~ \parentheses{-\ln p(x) - 1 -\lambda_1 -x \lambda_2}.
\end{aligned}$$

So we have that 

$$p(x) = \exp\parentheses{-1-\lambda_1-x\lambda_2}.$$

Next we enforce the constraints. First,

$$\begin{aligned}
1 &= \int dx~ p(x)\\
&= -\frac{1}{\lambda_2}\exp\parentheses{-1-\lambda_1-x\lambda_2} \bigg\rvert_{0}^\infty\\
&= \frac{1}{\lambda_2}\exp\parentheses{-1-\lambda_1}
\end{aligned}$$

where we now need that $\lambda_2>0$ so the integral is convergent. Then 

$$\lambda_2 = \exp\parentheses{-1-\lambda_1}.$$

Next, we need

$$\begin{aligned}
\mu &= \int dx~ x p(x)\\
&= \int_0^\infty dx~ x \exp\parentheses{-1-\lambda_1-x\lambda_2}\\
&= \frac{1}{\lambda_2^2}\exp\parentheses{-\lambda_1-1}
\end{aligned}$$

where the integral is performed with integration by parts. So

$$\mu \lambda_2^2 = \exp\parentheses{-\lambda_1-1}.$$

Combining these two constraints, we find $\lambda_2 = 1/\mu$ and $\lambda_1 = \ln \mu - 1.$ Plugging back in, we get

$$\begin{aligned}
p(x) &= \exp\parentheses{-\ln \mu - x/\mu}\\
&= \frac{1}{\mu} e^{-x/\mu},
\end{aligned}$$

which is indeed the exponential distribution.

*In summary*, the exponential distribution is the probability distribution that maximizes the entropy given a fixed mean. A similar calculation shows that the Gaussian distribution is the probability distribution that maximizes the entropy given a fixed mean and a fixed variance.


{% include post-footer.html %}
