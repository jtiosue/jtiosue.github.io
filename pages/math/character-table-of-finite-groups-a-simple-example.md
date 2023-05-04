---
title: Character table of finite groups - a simple example
comments: 36
---

{% include post-header.md %}

(04 May 2023) Consider the group presented as $G = \langle a, b \vert ab=-ba, a^2=b^2=1\rangle$. By multiplying in all combinations, we find that $|G|=8$ with $G= \{1,-1,a,-a,b,-b,ab,-ab\}$. One can check that there are five conjugacy classes:

$$
C(1) = \{1\},~ C(-1)=\{-1\},~C(a) = \{a,-a\},~C(b)=\{b,-b\},~C(ab)=\{ab,-ab\}.
$$

Therefore, there are five irreducible representations. Let $d_1,\dots,d_5$ be the dimensions of the representations. Then we know that $\sum_i d_i^2 = |G|=8$. The only way to satisfy this equation is $d_1=d_2=d_3=d_4=1$ and $d_5=2$. Thus, $G$ has four one-dimensional irreps and one two-dimensional irrep. 

Let $\rho_i$ be the irreps and $\chi_{\rho}$ be the character $\chi_\rho(g) = \mathrm{Tr}(\rho(g))$ which is constant inside a conjugacy class. Then we can construct the character table, where the columns correspond to conjugacy classes and the rows correspond to the irreps. Each element then corresponds to the character acting on that conjugacy class. The character table is square. The columns are orthogonal. Furthermore, the rows are orthogonal when weighting the dot product by the size of the conjugacy classes. 

The irreps can be determined by selecting values for $\rho_i(a)$ and $\rho_i(b)$ (and then using the homomorphism property of $\rho_i$). Since $\rho_i(a)^2 = \rho_i(b)^2=1$, we arrive at our four one-dimensional irreps by 

$$
\rho_1(a)=\rho_1(b) = 1, ~\rho_2(a) =-\rho_2(b) = 1,~-\rho_3(a)=\rho_3(b) = 1, ~-\rho_4(a)=-\rho_4(b) = 1.
$$

Finally, in order to make the rows of the character table orthogonal, we see (see the table below) that we must take $\chi_{\rho_5}(a) = \chi_{\rho_5}(b) = \chi_{\rho_5}(ab) = 0$. We easily find that the two-dimensional irrep is (up to isomorphism)

$$
\rho_5(a) = \begin{pmatrix}1&0\\0&-1\end{pmatrix} = \sigma_z, \qquad \rho_5(b) = \begin{pmatrix}0&1\\1&0\end{pmatrix} = \sigma_x.
$$

We therefore find that $G \cong \langle \sigma_x, \sigma_z \rangle$. The character table is as follows.

|  | $C(1)$ | $C(-1)$ | $C(a)$ | $C(b)$ | $C(ab)$ |
| --- | --- | --- | --- | --- | --- |
| $\chi_{\rho_1}$ | $1$ | $1$ | $1$ | $1$ | $1$ |
| $\chi_{\rho_2}$ | $1$ | $1$ | $1$ | $-1$ | $-1$ |
| $\chi_{\rho_3}$ | $1$ | $1$ | $-1$ | $1$ | $-1$ |
| $\chi_{\rho_4}$ | $1$ | $1$ | $-1$ | $-1$ | $1$ |
| $\chi_{\rho_5}$ | $2$ | $-2$ | $0$ | $0$ | $0$ |

One can check the properties discussed above. Namely the columns are orthogonal with respect to the dot product. The rows are orthogonal when weighted by the size of the conjugacy class; for example, take the weighted dot product between the first two rows to be $1\times 1+1\times 1+2(1\times 1) + 2(1\times -1)+2(1\times -1) = 0$.


{% include post-footer.html %}
