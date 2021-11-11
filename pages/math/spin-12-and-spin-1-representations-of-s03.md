---
title: Spin-1/2 and spin-1 representations of SO(3)
comments: 28
---

{% include post-header.md %}

(11 Nov 2021) In this post, I will show an explicit example of projective and linear representations of $\SO(3)$. Namely, we will construct projective unitary representations of $\SO(3)$ of arbitrary dimension, and then show that these representations are linear for all odd dimensions, but are not linear in even dimensions. We can then say that fermions are projective representations of $\SO(3)$ and bosons are linear representations.

In this post, we will take for granite that there is a surjective homomorphism $f\colon \SU(2) \to \SO(3)$ satisfying $\mathrm{Ker}(f) = \set{1,-1} \cong \bbZ_2$. Since $f$ is surjective, $\Im{f} = \SO(3)$. This comes from the fact that $\SU(2)$ is the universal covering group of $\SO(3)$, something that I will hopefully post about at some point in the future. More generally, there is a nice connection between projective representations of groups and linear representations of their covering groups. I will hopefully post about this someday.

By the fundamental homomorphism theorem, $\SU(2)/\mathrm{Ker}(f) \cong \Im{f} = \SO(3)$. Throughout this post, $h\colon \SU(2) / \bbZ_2 \to \SO(3)$ will be this isomorphism. Also, we will be considering elements of $\SO(3)$ to be matrices, so that $\SO(3) \subset \GL(3, \bbC)$.

We know that for each $n$, there is an irreducible representation of $\SU(2)$. Let's denote this by the map $\Pi_n\colon \SU(2) \to \GL(n,\bbC)$. Fix $X$ to be a set of representatives of $\SU(2) / \bbZ_2$. In other words, for each $g \in \SU(2)$, exactly one of $\set{g,-g}$ is in $X$. We define the map

$$
\begin{aligned}
\phi\colon &\SU(2) / \bbZ_2 \to \SU(2)\\
&g \bbZ_2 \mapsto \begin{cases}g&\text{if } g \in X\\-g&\text{if }-g \in X.\end{cases}
\end{aligned}
$$

Note that

$$\phi(g_i \bbZ_2)\phi(\g_j \bbZ_2) = c(g_i,g_j)\phi(g_i g_j \bbZ_2)$$

for some $c(g_i,g_j) \in \bbZ_2$. Define that map $\rho_n \coloneqq \Pi_n \circ \phi$ so that $\rho_n \colon \SU(2)/\bbZ_2 \to \GL(n,\bbC)$. Notice that

$$\begin{aligned}
\rho_n(g_i\bbZ_2) \rho_n(g_j \bbZ_2) &= \Pi_n(\phi(g_i\bbZ_2)) \Pi_n(\phi(g_j\bbZ_2)) \\
&= \Pi_n(\phi(g_i\bbZ_2) \phi(g_j\bbZ_2)) \qquad \text{since } \Pi_n \text{ is a homomorphism}\\
&= \Pi_n(c(g_i,g_j) \phi(g_i g_j \bbZ_2))\\
&= \Pi_n(c(g_i,g_j)) \Pi_n(\phi(g_i g_j \bbZ_2))\\
&= \Pi_n(c(g_i,g_j)) \rho_n(g_i g_j \bbZ_2)\\
&= c_n(g_i,g_j) \rho_n(g_i g_j \bbZ_2),
\end{aligned}$$

where we've defined $c_n(g_i,g_j) \coloneqq \Pi_n(c(g_i,g_j))$. Since $\Pi_n$ is a homomorphism, $\Pi_n(1) = 1$ and $\Pi_n(-1) = \pm 1$; hence, $c_n(g_i,g_j) \in \bbZ_2$. Therefore, we see that $\rho_n$ is indeed a projective unitary representation, so that $\rho_n \circ h^{-1}$ is a projective unitary representation of $\SO(3)$ on $\GL(n,\bbC)$. 


### The three dimensional representation is linear

In this section we will show that $\rho_3 \circ h^{-1}$ is a linear representation. Since $h$ is just an isomorphism, we just show that $\rho_3$ is a linear representation. This amounts to showing that $c_3(g_i,g_j)$ is always equal to 1. Hence, we just need to show that $\Pi_3(-1) = 1$. We can construct the irrep $\Pi_3$ explicitly as

$$\begin{aligned}
\Pi_3\colon &\SU(2) \to \GL(3,\bbC)\\
&g \mapsto h(g\bbZ_2).
\end{aligned}$$

Then $\Pi_3(-1) = h(-\bbZ_2) = h(\bbZ_2) = \Pi_3(1) = 1$, as desired. The only thing to confirm is that this explict representation $\Pi_3$ is indeed irreducible. To do this, we need to show that if $W \subset \bbC^3$ satisfies $Pi_3(g)W = W$ for all $g \in \SU(2)$, then $W = \set{0}$ or $\bbC^3$. Using our explicit form of $\Pi_3$, this amounts to showing that

$$(\forall R \in \SO(3)\colon R W = W) \implies W = \set{0} \text{ or } \bbC^3. $$

This is not too hard to show by just looking at the action of a rotation $R$ on the vector $\begin{pmatrix} \alpha&\beta&\gamma \end{pmatrix}^T$, and showing that any such vector will be rotated around the whole space $\bbC^3$.


### The two dimensional representation is not linear

In this section we will show that $\rho_2 \circ h^{-1}$ is not a linear representation. Since $h$ is just an isomorphism, we just show that $\rho_2$ is not a linear representation. This amounts to showing that $c_2(g_i,g_j)$ is not always equal to 1. Hence, we just need to show that $\Pi_2(-1) = -1$ and that $c(g_i, g_j)$ is sometimes equal to -1. 

The first part is easy. $\Pi_2$ is the fundamental representation, so that $\Pi_2(g) = g$. Hence, $\Pi_2(-1) = -1$. Next we show that $c(g_i,g_j)$ is not always 1.

In order for all $c(g_i,g_j) = 1$, we would need that $g_i,g_j \in X \implies g_ig_j \in X$. Suupose that $-1 \in X$. Then this implies that $g \in X \implies -g \in X$. But this contradicts our definition of $X$. Therefore, $-1 \notin X$, and we must instead have $1 \in X$. 

Consider the matrix $R(\theta) \coloneqq \mathrm{diag}\pargs{\e^{\i\theta}, \e^{-\i\theta}}$. Suppose that $R(\theta) \in X$, which implies that $-R(\theta) = R(\theta + \pi) = R(\theta-\pi) \notin X$. The condition that $g_i,g_j \in X \implies g_ig_j \in X$ implies that $g \in X \implies g^m \in X$ for any integer $m$. As such, $R(\theta)^m = R(m\theta) \in X$. Suppose $R(\pi/2) \in X$, then $R(2 \pi/2) = R(\pi) = -1 \in X$, which is a contradiction since we already showed that $-1 \notin X$. Therefore, $R(\pi/2) \notin X$, meaning that $-R(\pi/2) = R(\pi/2 - \pi) = R(-\pi/2) \in X$. This then implies that $R(2(-\pi/2)) = R(-\pi) = -1 \in X$, which is again a contradiction. 

We have thus shown that $c(g_i,g_j)$ is not always 1, completing the proof that $\rho_2 \circ h^{-1}$ is not a linear representation, but instead only a projective unitary representation.



{% include post-footer.html %}
