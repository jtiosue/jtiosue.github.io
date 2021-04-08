---
title: The origin of the name POVM
comments: 2
---

{% include post-header.md %}

(16 Jan 2021) A Positive Operator-Valued Measure (POVM) is a generalized measurement on a quantum system. I have always wondered where the name comes from, and here I will give a rough description of its origin. We'll begin by reviewing what a generalized quantum measurement is. Then we'll discuss where it gets its name.

## Generalized quantum measurement

To measure non orthogonal quantum states, we must perform some operation on the system plus an ancilla system so that what we want to measure becomes orthogonal, in which case a standard projective measurement can be done. There are operators $\{ M_a\}$ such that:

$$U: \vert\psi\rangle\otimes \vert 0 \rangle \to \sum_a \parentheses{M_a \vert \psi\rangle} \otimes \vert a \rangle$$

$$U$ must be unitary, so

$$\begin{aligned}
1 &= \left\lvert\left\lvert\sum_a \left(M_a \vert\psi\rangle \right)\otimes \vert a\rangle\right\rvert\right\rvert^2\\
&= \sum_{a, b} \langle a\vert b\rangle \langle\psi\vert M_a^\dagger M_a \vert\psi\rangle.
\end{aligned}$$

This implies that $\sum_a M_a^\dagger M_a = I$.

The $\{M_a \}$ are called Krauss operators. A set $\{E_a \} = \{M_a^\dagger M_a \}$ constitutes a POVM measurement. We see clearly that each $E_a$ is Hermitian, and it is also positive semidefinite because $E_a$ has a set of orthornormal eigenvectors $\{\vert\psi_a \rangle \}$ with corresponding eigenvalues $\lambda_a$, where

$$\begin{aligned}
0 &\leq \left\lvert\left\lvert M_a \vert\psi_a\rangle\right\rvert\right\rvert^2\\
&= \langle\psi_a\vert M_a^\dagger M_a \vert\psi_a\rangle\\
&= \langle \psi_a\vert E_a \vert\psi_a\rangle\\
&= \lambda_a.
\end{aligned}$$

Thus the eigenvalues of $E_a$ are greater than or equal to 0 (if the equality couldn't hold than they would be positive definite).

### Quantum channel

The quantum channel corresponding to the POVM is $\mathcal{E}: \rho \mapsto \sum_a M_a \rho M_a^\dagger$. $\mathcal{E}$ is a quantum channel, superoperator, or trace preserving completely postive map. A superoperator performs arbitrary mixed state evolution when coupled to an environment (non unitary! Of course on the entire system + environment it is unitary evolution, but it is non unitary on the system). The trace of $\rho$ is conserved so this formalism for mixed state evolution conserves probability. We see that it preserves the trace because we can use the linearity of the trace and that the trace is invariant under cyclic permutations to get,

$$\begin{aligned}
\Tr\mathcal{E}(\rho) &= \Tr \left(\sum_a M_a \rho M_a^\dagger \right)\\
&= \sum_a\Tr\left( M_a \rho M_a^\dagger \right)\\
&= \sum_a \Tr\left(M_a^\dagger M_a \rho \right)\\
&= \Tr\left(\sum_{a} M_a^\dagger M_a \rho \right)\\
&= \Tr \left(I \rho \right)\\
&= \Tr \rho
\end{aligned}$$

### Measurement probability outcomes

From this formalism, we can see that if we associate each $E_a$ with a measurement outcome $a$, then then probability of measuring $a$ is just $\textrm{Pr}(a) = \Tr E_a \rho$, and thus the post measurement state is $\rho' = \frac{M_a \rho M_a^\dagger}{\textrm{Pr}(a)}$.


## Origin of the name POVM

With the brief review, let's now discuss what a Positive Operator-Valued Measure is. We are used to measures of the form $\mu: \Sigma \to [0, \infty) \cup \{\infty \}$. A POVM is a measure whose codomain is instead a postive operator.

Let's call our Hilbert Space $H$. Let $P(H)$ denote the set of positive bounded operators on $H$. Let $A$ be the set of possible measurement outcomes. Finally let $B(A)$ be the Borel Sigma Algebra of the set $A$ (the set of all measureable subsets of $A$). The a POVM $E$ is a map $E: B(A) \to P(H)$ that satisfies

- $E(A) = I$ (normalized),
- $E(\emptyset) = 0$,
- For all $A_i \in B(A)$ such that $A_i \cap A_j = \emptyset$, we have that $E\parentheses{\bigcup_{i\in S} A_i} = \sum_{i\in S} E(A_i)$, where $S \subseteq \mathbb N$ ($\sigma$$-additive for finite and/or *countable* unions).

Then we can associate a standard measure $\mu_E: B(A) \to [0, 1]$ to the POVM $E$ where $\mu_E(\mathcal A) = \Tr E(\mathcal A)\rho$ which is precisely equivalent to $\sum_{a\in\mathcal A}\textrm{Pr}(a)$$!

Let's go to two examples.

### Example: spin-1 particle

*Thanks to this [StackExchange post](https://physics.stackexchange.com/a/139117/114833) that finally cleared POVMs up for me with an example similar to this one.*

Consider that we have a spin-1 particle, and let's say that we want to measure the spin of the particle. Then our measurement outcomes are $A = \{-1, 0, 1 \}$. Then we have

- $E(A) = E(\{-1, 0, 1 \}) = I$,
- $E(\emptyset) = 0$,
- $E(\{1 \}) = E_1$ for some positive operator $E_1$ (e.g. $E_1 = \lvert \uparrow \rangle \langle \uparrow \rvert$),
- $E(\{-1 \}) = E_{-1}$ for some positive operator $E_{-1}$ (e.g. $E_{-1} = \lvert \downarrow \rangle \langle \downarrow \rvert$),
- $E(\{0 \}) = E(A) - E(\{-1 \}) - E(\{1 \}) = E_{0}$ for the positive operator $E_{0} \coloneqq I - E_{-1} - E_1$,
- $E(\{0, 1 \}) = E(\{0 \}) + E(\{1 \}) = E_0 + E_1$,
- $E(\{-1, 1 \}) = E(\{-1 \}) + E(\{1 \}) = E_{-1} + E_1$,
- $E(\{-1, 0 \}) = E(\{-1 \}) + E(\{0 \}) = E_{-1} + E_0$.

Then we see that the probability of measuring the spin of the particle to be $0$ is

$$\begin{aligned}
\textrm{Pr}(0) &= \mu_E(\{0 \})\\
&= \Tr E(\{0 \}) \rho\\
&= \Tr E_0 \rho.
\end{aligned}$$

Similarly, the probability of measuring the spin of the particle to either $-1$ or $1$ is

$$\begin{aligned}
\textrm{Pr}(-1) + \textrm{Pr}(1) &= \mu_E(\{-1, 1 \})\\
&= \Tr E(\{-1, 1 \}) \rho\\
&= \Tr(E_{-1} + E_1)\rho.
\end{aligned}$$

And the probability of measuring the spin to be *something* is

$$\begin{aligned}
\textrm{Pr}(-1) + \textrm{Pr}(0) + \textrm{Pr}(1) &= \mu_{E}(\{-1, 0, 1 \})\\
&= \Tr E(\{-1, 0, 1 \})\rho\\
&= \Tr I \rho = 1.
\end{aligned}$$

Thus we see that a POVM is like a measure that returns a positive operator, and can be associated to a normal measure that then gives us the corresponding probability of measuring an event.


### Example: position of particle in one dimension

Now equipped with a measure, we can talk about when the POVM has infinitely many possible measurement outcomes (*I'm not totally sure if this example is correct; I tried to think of an example of when $\lvert A\rvert$ is infinite, but I could be wrong here, there are potentially more complications since I think we're technically now working in a rigged Hilbert Space, and I don't think* $\vert x\rangle\langle x \vert \in P(L^2(\mathbb R))$).

Consider now a particle in one dimension along the $x$ axis. We want to determine the probability of finding the particle in a particular region. The set of measurement outcomes then is $(-\infty, \infty) = \mathbb R$. The POVM is $E: B(\mathbb R) \to P(L^2(\mathbb R))$, with 

$$\begin{aligned}
E([x, x+dx]) &= \int_x^{x+dx} \vert y \rangle \langle y \vert dy\\
&\approx \vert x \rangle \langle x \vert dx
\end{aligned}$$

for all $x \in \mathbb R$. Notice that

$$E(\mathbb R) = \int_{-\infty}^\infty \vert y \rangle \langle y \vert dy = I$$

since the (generalized) position eigenstates form a basis (to be more precise, we need more concepts from rigged Hilbert Spaces).

Let's assume that the state $\rho = \vert \psi \rangle\langle\psi \vert$ is a pure state. Then the probability that we find the particle, let's say, in the interval $[y, y+dy] \subset \mathbb R$ is

$$\begin{aligned}
\textrm{Pr}([y,y+dy]) &= \mu_E([y,y+dy])\\
&\approx \Tr \left[\rho \vert y\rangle\langle y\vert dy \right]\\
&= dy \Tr \left[\vert \psi \rangle\langle \psi \vert y\rangle\langle y\vert\right]\\
&= \left\lvert\langle y\vert \psi\rangle \right\rvert^2 dy
\end{aligned}$$

We can calculate, for example, the average position via the following Lebesgue integral:

$$\begin{aligned}
\angles x &= \int_{\mathbb R} x d\mu_E(x)\\
&= \int_{\mathbb R} x \Tr\left[E([x, x+dx]) \rho \right]\\
&= \int_{\mathbb R} x \Tr\left[dx \vert x\rangle\langle x\vert \rho \right]\\
&= \int_{-\infty}^\infty x \Tr\left[\vert x\rangle\langle x\vert \psi\rangle\langle \psi\vert \right] dx\\
&= \int_{-\infty}^\infty x \left\lvert\langle x\vert \psi\rangle \right\rvert^2 dx.\\
\end{aligned}$$


### Example: position of particle in two dimensions

*Similar to the previous example, I could be a little wrong here, or at least a little imprecise.*

Next we consider a particle somewhere in the $(x, y)$$-plane. The POVM is $E: B(\mathbb R^2) \to P(L^2(\mathbb R^2))$ (recall that $L^2(\mathbb R^2) = L^2(\mathbb R) \otimes L^2(\mathbb R)$), with

$$\begin{aligned}
E([x, x+dx] \times [y, y+dy]) &= \int_x^{x+dx}\int_y^{y+dy} \vert x' \rangle \langle x' \vert \otimes \vert y' \rangle \langle y' \vert dx'dy'\\
&\approx \vert x \rangle \langle x \vert \otimes \vert y \rangle \langle y \vert dx dy
\end{aligned}$$

for all $x, y \in \mathbb R$. Indeed we see that this is a product measure using the measure from the previous exmaple. Let's assume that the state $\rho = \vert \psi \rangle\langle\psi \vert$ is a pure state. Then the probability that we find the particle, let's say, in a patch $[x, x+dx] \times [y, y+dy] \subset \mathbb R^2$ is

$$\begin{aligned}
\textrm{Pr}([x, x+dx] \times [y,y+dy]) &= \mu_E([x, x+dx] \times [y,y+dy])\\
&\approx \Tr \left[\rho \vert x\rangle\langle x\vert \otimes \vert y\rangle\langle y\vert dx dy \right]\\
&= dxdy \Tr \left[\vert \psi \rangle\langle \psi \vert \left(\vert x\rangle\langle x\vert\otimes \vert y\rangle\langle y\vert\right)\right]\\
&= \left\lvert\langle \psi\vert \left(\vert x \rangle \otimes \vert y \rangle \right) \right\rvert^2 dx dy
\end{aligned}$$

We can calculate, for example, the average square distance from the origin via the following Lebesgue integral:

$$\begin{aligned}
\angles{x^2 + y^2} &= \int_{\mathbb R^2} (x^2+y^2) d\mu_E(x, y)\\
&= \int_{\mathbb R^2} (x^2+y^2) \Tr\left[E([x, x+dx] \times [y,y+dy]) \rho \right]\\
&= \int_{\mathbb R^2} (x^2+y^2) \Tr\left[dxdy \vert x\rangle\langle x\vert \otimes \vert y\rangle\langle y\vert \rho \right]\\
&= \int_{-\infty}^\infty\int_{-\infty}^\infty (x^2+y^2) \left\lvert\left(\langle x\vert \otimes \langle y\vert \right) \vert \psi\rangle \right\rvert^2 dx.\\
\end{aligned}$$

So we have reproduced the well-known results from quantum mechanics.


{% include post-footer.html %}
