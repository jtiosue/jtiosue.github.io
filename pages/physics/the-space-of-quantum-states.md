---
title: The space of quantum states
comments: 25
---

{% include post-header.md %}

(07 Jul 2021) Denote the set of all pure quantum states on an $n$-dimensional Hilbert space as $S$. Every pure quantum state is a unit vector in $\bbC^n$. As a real vector space, $\bbC^n \cong \bbR^{2n}$. A unit vector in $\bbR^{2n}$ lives on the sphere $\text S^{2n-1}$. Therefore, we are tempted to say that $S \cong \text S^{2n-1}$. However, pure states come along with the equivalence relation $\sim$ denoting the irrelevance of a global phase factor; $\ket \psi \sim e^{i \theta} \ket \psi$. Thus, $S \cong \text S^{2n-1} / \mathord \sim$. Equivalently, $S \cong \text S^{2n-1} / \text U(1)$ where $\text U(1)$ is the one-dimensional unitary group. This is exactly the definition of the complex projective space $\bbC \bbP^{n-1}$. So we finally conclude that

$$S \cong \bbC \bbP^{n-1}.$$

Denote the set of all mixed quantum states (i.e. density matrices) on an $n$-dimensional Hilbert space as $D$. Any mixed state can be written as $\rho = \sum_i p_i \ketbra{i}{i}$ for an orthonormal basis $\set{\ket i}$. Such a $\rho$ can be purified as $\ket \psi = \sum_i \sqrt{p_i}\ket i \otimes \ket j$ for an orthonormal basis $\set{\ket j}$. $\psi$ is an $n^2$-dimensional pure state, so we are tempted to say that $D \cong \bbC\bbP^{n^2-1}$. However, we also know that $\rho$ could have just as well been purified as $\ket \psi = \sum_i \sqrt{p_i}\ket i \otimes U\ket j$ for any unitary $U \in \text U(n)$. Therefore, $D \cong \bbC\bbP^{n^2-1}/ \text U(n)$. But we already divided out by $\text U(1)$ in the definition of $\bbC\bbP^{n^2-1}$. Therefore,

$$D \cong \bbC\bbP^{n^2-1}/ \text{SU}(n).$$


{% include post-footer.html %}
