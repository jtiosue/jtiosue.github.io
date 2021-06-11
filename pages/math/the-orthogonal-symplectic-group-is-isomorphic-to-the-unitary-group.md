---
title: The orthogonal symplectic group is isomorphic to the unitary group
comments: 24
---

{% include post-header.md %}

(11 June 2021) The orthogonal group is

$$\text O(n) = \set{M \in \bbR^{n\times n} \mid M^T M =MM^T = I}.$$

The unitary group is

$$\text U(n) = \set{M \in \bbC^{n\times n} \mid M^\dagger M = MM^\dagger = I}.$$

The symplectic group is 

$$\text{Sp}(2n) = \set{M \in \bbR^{2n \times 2n} \mid M \Omega M^T = \Omega}$$

where $\Omega$ is the symplectic form

$$\Omega = \begin{pmatrix} 0_{n\times n}&I_{n\times n}\\ -I_{n\times n}&0_{n\times n} \end{pmatrix}.$$

The orthogonal symplectic group is 

$$\text K(n) = \text{Sp}(2n) \cap \text O (2n).$$

In [this post of mine](on-the-compactness-of-the-unitary-orthogonal-and-symplectic-groups.md), we proved that $\text O(n), \text U(n),$ and $\text K(n)$ are all compact, while $\text{Sp}(2n)$ is not compact. In this post, we will prove that $U(n)$ and $K(n)$ are isomorphic.


**Lemma 1**. $U=A+iB$ for $n\times n$ real matrices $A$ and $B$ is unitary if and only if $AA^T+BB^T=I$, $A^T A+B^T B = I$, and $AB^T$ and $A^T B$ are symmetric.

*Proof:*

$$\begin{aligned}
U^\dagger U &= (A^T - i B^T)(A+iB)\\
&= A^T A + B^T B +i (A^T B - B^T A)\\
UU^\dagger &= (A+iB)(A^T - i B^T)\\
&= AA^T + BB^T + i(BA^T - AB^T).
\end{aligned}$$

These equal the identity iff the conditions are met. {% include endproof.html %}


**Lemma 2**. $M \in K(n) \iff$

$$M = \begin{pmatrix}A&-B\\B&A \end{pmatrix}$$

for $n\times n$ real matrices $A$ and $B$ satisfying $AA^T+BB^T=I$, $A^T A+B^T B = I$, and $AB^T$ and $A^T B$ are symmetric.

*Proof:* Start with the $(\Rightarrow)$ direction. Let 

$$M = \begin{pmatrix} A&-B\\C&D\end{pmatrix} \in \text K(n).$$ 

Then $M\Omega M^T = \Omega $ since $M \in \text{Sp}(2n)$. Multiply both sides on the right by $M$; since $M \in \text{O}(2n)$, this becomes $M\Omega  = \Omega M$. Simple matrix multiplication on this equation confirms that $A=D$ and $B=C$. Thus, 

$$M = \begin{pmatrix} A&-B\\B&A\end{pmatrix}.$$ 

We then only need confirm that $A$ and $B$ satisfy the conditions. Again, multiplying out $M\Omega M^T = \Omega $ and $M^T \Omega  M = \Omega $ confirms that the conditions are met.

Now we do the $(\Leftarrow)$ direction. Let 

$$M = \begin{pmatrix}A&-B\\B&A \end{pmatrix}.$$ 

Simple matrix multiplication confirms that when $A$ and $B$ satisfy the conditions, $MM^T = M^TM = I$ and $M\Omega M^T = \Omega $. Thus, $M \in \text K(n)$. {% include endproof.html %}


**Theorem**. The map $\phi\colon U(n) \to K(n)$ defined by 

$$\phi(U) = \begin{pmatrix}\Re U&-\Im U\\\Im U&\Re U \end{pmatrix}$$

is an isomorphism.

*Proof:* Lemma 1 and 2 together prove that $M \in K(n)$ iff $M = \phi(U)$ for some unitary matrix $U$. Combining this with the obvious fact that $\phi$ is injective implies that $\phi$ is bijective. By just expanding out the multiplication, one finds that $\phi$ is a homomorphism. Combining this with the fact that a bijective homomorphism is always an isomorphism when dealing with groups, we find that $\phi$ is an isomorphism.

For completeness, suppose we didn't know that a bijective homomorphism is always an isomorphism when dealing with groups. Then we would simply need to prove that $\phi^{-1}$ is a homomorphism. This is again straightforward to check via direct multiplication. {% include endproof.html %}



#### References

- M. A. de Gosson. *Symplectic Geometry and Quantum Mechanics*. Advances in Partial Differential Equations. Birkhäuser Basel, 2006.


{% include post-footer.html %}
