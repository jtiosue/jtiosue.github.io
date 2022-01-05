---
title: Addition of angular momentum, a simple example
comments: 27
---

{% include post-header.md %}

(11 Nov 2021) This post will be a brief example of decomposing a tensor product of two two-dimensional representations of $\SU(2)$ into a direct sum of a one-dimensional and three dimensional representation. In other words, we decompose the tensor product space of two spin-1/2 particles into a direct sum of a spin-0 particle and a spin-1 particle. Throughout this post, $\vec{\sigma} = (\sigma^x,\sigma^y,\sigma^z)$ will denote the Pauli matrices.

Suppose we have two spin-1/2 particles. Then the wavefunction lives in the space $V = \bbC^2 \otimes \bbC^2$. The fundamental representation is

$$\rho\colon \SU(2) \to \GL(\bbC^2),$$

where $\rho(g)$ is the $2\times 2$ matrix representing $g$. The tensor product representation is

$$\Pi\colon \SU(2) \to \GL(V), g \mapsto \rho(g)\otimes \rho(g). $$

Let's fix a, as we will see, nice orthonormal basis of $V$, namely $V = \mathrm{span}\cbargs{\ket{\psi_0},\ket{\psi_1},\ket{\psi_2},\ket{\psi_3}}$, where (I'm ignoring normalization)

$$
\begin{aligned}
\ket{\psi_0} &= \ket{01} - \ket{10}\\
\ket{\psi_1} &= \ket{00}\\
\ket{\psi_2} &= \ket{01} + \ket{10}\\
\ket{\psi_3} &= \ket{11}.
\end{aligned}
$$

Define $W \coloneqq \mathrm{span}\cbargs{\ket{\psi_0}}$, and recall that $V = W \oplus W^\perp$. We will show that $W$ and $W^\perp$ are invariant subspaces under the action of $\Pi(\SU(2))$. Consider, for example, $R_x(\theta) = \e^{\i \theta \sigma^x} \in \rho(\SU(2))$, and consider the action of $R_x(\theta) \otimes R_x(\theta) \in \Pi(\SU(2))$ on $W$. We have that

$$
\begin{aligned}
R_x(\theta) \otimes R_x(\theta) \ket{\psi_0} &= \parentheses{\cos\theta + \i \sin\theta \sigma^x}\otimes \parentheses{\cos\theta + \i \sin\theta \sigma^x} \ket{\psi_0}\\
&= \parentheses{\cos^2\theta + \i\cos\theta\sin\theta \brackets{\sigma^x \otimes 1 + 1\otimes \sigma^x} - \sin^2\theta \sigma^x \otimes \sigma^x} \ket{\psi_0}\\
&= \cos^2\theta \ket{\psi_0} + \i\cos\theta\sin\theta \brackets{\ket{11}-\ket{00} + \ket{00}-\ket{11}} - \sin^2\theta \brackets{\ket{10}-\ket{01}}\\
&= \parentheses{\cos^2\theta + \sin^2\theta} \ket{\psi_0}\\
&= \ket{\psi_0}.
\end{aligned}
$$

Indeed one can perform similar calculations for any arbitrary $\e^{\i \vec{\theta} \cdot \vec{\sigma}} \in \rho(\SU(2))$ and find that $\Pi(\SU(2)) W = W$. Therefore, $W$ *is an invariant subsapce*, which also implies that $W^\perp$ is also an invariant subspace. 

In general, what we find is that for any $g \in \SU(2)$, $\Pi(g)\ket{\psi_0} = \ket{\psi_0}$. Hence, $\Pi$ is the trivial representation $\Pi_{\rm trivial}$ when restricted to $W \subset V$, where $\Pi_{\rm trivial}(g) = \bbI$ for all $g$.

One can go through the same calculations and find that there is no invariant subspace of $W^\perp$ (except of course $\set{0}$ and $W^\perp$ itself) under the action of $\Pi(\SU(2))$. Thus, $\Pi$, when restricted to $W^\perp$, is a three-dimensional irreducible representation. 

Let's review what we've found. The space of two spin-1/2 particles $V$ can be decomposed as $V = W \oplus W^\perp$, where $W$ and $W^\perp$ are one and three dimensional subspaces of $V$ that are invariant under the action of $\SU(2)$. Hence, the space of two spin-1/2 paricles can be decomposed into a direct sum of the one and three dimensional irreps of $\SU(2)$. As such, the state $\ket{\psi_0}$ transforms as a spin-0 particle and the space $W^\perp$ is a spin-1 particle.

This is the origin of the notation $\ket{0,0} \equiv \ket{\psi_0}$, $\ket{1,1} \equiv \ket{\psi_1}$, $\ket{1,0} \equiv \ket{\psi_2}$, and $\ket{1,-1} \equiv \ket{\psi_3}$. The first number denotes the irrep that the state lives in (i.e. $\ket{0,0}$ lives in the spin-0 irrep and $\ket{1,m}$ lives in the spin-1 irrep). The second number denotes the eigenvalue of the total $z$ angular momentum $\frac{1}{2}\parentheses{\sigma^z\otimes 1 + 1 \otimes \sigma^z}$.


{% include post-footer.html %}
