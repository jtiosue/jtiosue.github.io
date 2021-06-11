---
title: On the compactness of the unitary, orthogonal, and symplectic groups
comments: 23
---

{% include post-header.md %}

(01 Jun 2021) In this post, I will prove that the unitary, orthogonal, and orthogonal symplectic groups are compact. Compactness of these groups is important in order to talk about integrating over the groups with the Haar measure.

The space of real $n \times n$ matrices $\bbR^{n\times n}$ is a subset of the $n^2$ dimensional Euclidean space $\bbR^{n^2}$ (i.e. metric space with the Euclidean metric) by considering each entry of the matrix as a coordinate. Similarly the space of complex $n \times n$ matrices $\bbC^{n \times n}$ is a subset of the $2n^2$ dimensional Euclidean space $\bbR^{2n^2}$ by considering the real and imaginary parts of the entries of the matrix as coordinates. Since the space of matrices is Euclidean, we can use the Heine-Borel theorem to prove compactness. Namely, we need only show closeness and boundedness in order to prove compactness. See [this post of mine](compactness-on-topological-spaces-and-why-it-is-important.html) for more info.


### The orthogonal group

The orthogonal group is

$$O(n) = \set{M \in \bbR^{n\times n} \mid M^T M = MM^T = I}.$$

Note that each entry of a matrix in $O(n)$ is between $-1$ and $1$ since the columns are orthonormal. Thus, for two matrices $A, B \in O(n)$,

$$\begin{aligned}
  d_{\text E}(A, B)^2 &= \sum_{i,j=1}^n (A_{ij}-B_{ij})^2\\
  &\leq 2n^2.
\end{aligned}$$

Therefore, $O(n)$ is bounded. Now we must prove that $O(n)$ is closed. To do this, we use Lemma 1 from [this post of mine](compactness-on-topological-spaces-and-why-it-is-important.html), which states that for a continuous function the preimage of a closed set is closed. We can consider the continuous function

$$\begin{aligned}
  f\colon ~&\bbR^{n\times n} \to \bbR^{n\times n}\\
  &A \mapsto A^T A.
\end{aligned}$$

Note that $\set{I}$ is closed and the preimage $f^{-1}\bargs{\set{I}} = O(n)$. Thus, by the Lemma, $O(n)$ is closed. Therefore the orthogonal group is compact.


### The unitary group

The unitary group is

$$U(n) = \set{M \in \bbC^{n\times n} \mid M^\dagger M = MM^\dagger = I}.$$

Note that each entry of a matrix in $U(n)$ has magnitude between $0$ and $1$ since the columns are orthonormal. Thus, for two matrices $A, B \in U(n)$,

$$\begin{aligned}
  d_{\text E}(A, B)^2 &= \sum_{i,j=1}^n (\Re A_{ij}- \Re B_{ij})^2 + \sum_{i,j=1}^n (\Im A_{ij}- \Im B_{ij})^2\\
  &= \sum_{i,j=1}^n \abs{A_{ij}- B_{ij}}^2\\
  &\leq 2n^2.
\end{aligned}$$

Therefore, $U(n)$ is bounded. Now we must prove that $U(n)$ is closed. To do this, we consider the continuous function

$$\begin{aligned}
  f\colon ~&\bbC^{n\times n} \to \bbC^{n\times n}\\
  &A \mapsto A^\dagger A.
\end{aligned}$$

Note that $\set{I}$ is closed and the preimage $f^{-1}\bargs{\set{I}} = U(n)$. Thus, by the Lemma, $U(n)$ is closed. Therefore, the unitary group is orthogonal.


### The symplectic group

The symplectic group is 

$$\text{Sp}(2n) = \set{M \in \bbR^{2n \times 2n} \mid M \Omega M^T = \Omega}$$

where $\Omega$ is the symplectic form

$$\Omega = \begin{pmatrix} 0_{n\times n}&I_{n\times n}\\ -I_{n\times n}&0_{n\times n} \end{pmatrix}.$$

$\text{Sp}(2n)$ is closed because it is the preimage of $\set{\Omega}$ under the continuous map $f\colon A \mapsto A \Omega A^T$. However, $\text{Sp}(2n)$ is not bounded, and is therefore not compact. We can see this by noticing that for every $a \neq 0$,

$$A_a \coloneqq \begin{pmatrix}aI_{n\times n}&0_{n\times n}\\0_{n\times n}& \frac{1}{a} I_{n \times n} \end{pmatrix}$$

is in $\text{Sp}(2n)$, because $A_a \Omega A_a = \Omega$. Then

$$\begin{aligned}
  d_{\text{E}}(A_a, A_b)^2 &= n(a-b)^2 + n(1/a-1/b)^2\\
  &\geq (a-b)^2
\end{aligned}$$

which is unbounded on $\bbR\setminus \cbargs 0$. Thus there is no Haar measure on the symplectic group since it is not compact. However, the group

$$K(n) \coloneqq \text{Sp}(2n) \cap O(2n)$$

is compact. The boundedness follows from the fact that $O(2n)$ is bounded. The closedness follows from the fact that both $\text{Sp}(2n)$ and $O(n)$ are closed and that the intersection of closed sets is closed. Therefore $K(n)$ is compact, and a Haar measure can be defined on it.

**Lemma:** The intersection of two closed sets is closed.

*Proof*: Suppose $A, B \subset X$ are closed sets in the topological space $X$. Then $A^c = X \setminus A$ and $B^c = X \setminus B$ are open. By definition of a topological space, $A^c \cup B^c$ is open and therefore $(A^c \cup B^c)^c$ is closed. Then by De Morgan's laws, $A \cap B = (A^c \cup B^c)^c$, so that $A \cap B$ is closed. {% include endproof.html %}



#### References

- [ON THE TOPOLOGY OF CERTAIN MATRIX GROUPS](https://www.jnu.ac.in/Faculty/vedgupta/matrix-gps-gupta-mishra.pdf)
- [https://www.maths.tcd.ie/pub/Maths/Courseware/GroupRepresentations/GpReps-II.pdf](https://www.maths.tcd.ie/pub/Maths/Courseware/GroupRepresentations/GpReps-II.pdf)


{% include post-footer.html %}
