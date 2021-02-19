---
title: Levi-Civita, determinants, volumes, and Jacobians
comments: 6
---

{% include post-header.md %}

(24 Jan 2021) Here we will discuss the relationship between the determinant and volumes, something that semi-confused me for a while. My discussion here is largely derived from my reading of [this excellent textbook](https://www.amazon.com/Introduction-Tensors-Group-Theory-Physicists/dp/3319147935) and [this StackExchange post](https://math.stackexchange.com/a/547522/395731).

Fix a vector space $$V$$ over the field $$\mathbb F \in \{\mathbb R, \mathbb C \}$$ with an orthonormal basis $$\{e_i ~\mid~ i=1,\dots,\textrm{dim}V \}$$. $$V^*$$ is the corresponding dual space - i.e. the set of all linear functionals from $$V$$ to $$\FF$$. $$\{e^i \}$$ is the corresponding dual basis, defined so that $$e^i(e_j) = \delta^i_j$$. Recall that the space 

$$\underbrace{V^* \otimes \dots \otimes V^*}_{r \textrm{ times}} \otimes \underbrace{V \otimes \dots \otimes V}_{s \textrm{ times}}$$

is the set of all $$\mathbb F$$-valued multilinear functions on 

$$\underbrace{V \times \dots \times V}_{r \textrm{ times}} \times \underbrace{V^* \times \dots \times V^*}_{s \textrm{ times}}.$$

Thus it is the vector space of all rank $$(r, s)$$ tensors. It is spanned by the basis 

$$\begin{aligned}
\{e^{i_1} \otimes \dots\otimes e^{i_r} \otimes e_{j_1} \otimes \dots \otimes e_{j_s} & \mid \\
i_k, j_k =1, \dots, \textrm{dim}V & \}.
\end{aligned}$$

For example,

$$\begin{aligned}
(e^i \otimes e_j):& V \times V^* \to \FF\\
&(e_k, e^\ell) \mapsto e^i(e_k) e_j(e^\ell) = \delta^i_k \delta^\ell_j.
\end{aligned}$$

Any tensor $$T$$ can then be expressed (using summation convension) as

$$T = T_{i_1\dots i_r}^{~~~~~~~~j_1 \dots j_s } e^{i_1} \otimes \dots\otimes e^{i_r} \otimes e_{j_1} \otimes \dots \otimes e_{j_s}.$$

### The Levi-Civita tensor

An antisymmetric $$(r, 0)$$ or $$(0, s)$$ tensor changes sign when exchanging any two of its arguments. The Levi-Civita tensor

$$\epsilon: \underbrace{V \times \dots \times V}_{n\coloneqq \textrm{dim}V \textrm{ times}} \to \mathbb F$$

is a totally antisymmetric $$(\textrm{dim}V, 0)$$ tensor. Notice that once we define $$\epsilon(e_1, \dots, e_n)$$, then we have uniquely specified $$\epsilon$$, since we can determine its action on every other set of inputs by swapping inputs and adding minus signs. For example,

$$\epsilon(e_3, e_1, e_2) = -\epsilon(e_1, e_3, e_2) = \epsilon(e_1, e_2, e_3).$$

Since it is multilinear, it is enough to specify its action on inputs from the basis. The Levi-Civita tensor is typically defined such that $$\epsilon(e_1, \dots, e_n) = 1$$. Since $$\epsilon$$ is antisymmetric, $$\epsilon(v_1, \dots, v_n) = 0$$ if any $$v_i = v_j$$ when $$i \neq j$$.

For example, if $$\textrm{dim}V = 2$$, then 

$$\epsilon = e^{1} \otimes e^2 - e^2 \otimes e^1.$$

If $$\textrm{dim}V = 3$$, then 

$$\begin{aligned}
\epsilon &= e^1 \otimes e^2\otimes e^3 + e^2\otimes e^3\otimes e^1 + e^3\otimes e^1\otimes e^2\\
&~ - e^1\otimes e^3\otimes e^2 - e^3\otimes e^2\otimes e^1 - e^2\otimes e^1\otimes e^3.
\end{aligned}$$

### Determinant

Consider an $$n \times n$$ matrix $$A$$ with components $$A_{ij}$$. Denote the $$i^{\textrm th}$$ column vector of $$A$$ as $$A_i$$, so that 

$$A_i \coloneqq \left(\begin{matrix}A_{1i}\\\vdots\\A_{ni} \end{matrix}\right).$$ 

Then the determinant of $$A$$ is defined as

$$\det(A) \coloneqq \epsilon(A_1, \dots, A_n) = \sum_{\sigma\in S_n}\textrm{sgn}(\sigma)\prod_{i=1}^n A_{\sigma(i)i}.$$

Recall the sign of a permutation is $$\textrm{sgn}(\sigma) = (-1)^{\xi(\sigma)}$$ where $$\xi(\sigma)$$ is the number of transpositions of two elements to get back to the trivial permutation. Indeed $$\textrm{sgn}(\sigma) = \epsilon(e_{\sigma(1)}, \dots, e_{\sigma(n)})$$.

#### Properties

Fix $$n \times n$$ matrices $$A, B$$.

**Property 1**: $$\det(A B) = \det(A)\det(B)$$.

*Proof*: The $$i^{\textrm{th}}$$ column of $$B$$ can be written as $$B_i = B_{ji}e_j$$.

$$\begin{aligned}
\det AB &= \epsilon\left(AB_1, \dots, AB_n \right)\\
&= \epsilon\left(AB_{j_1 1} e_{j_1}, \dots, AB_{j_n n}e_{j_n} \right)\\
&= B_{j_1 1} \dots B_{j_n n}\epsilon\left(A e_{j_1}, \dots, A e_{j_n} \right)\\
&= B_{j_1 1} \dots B_{j_n n} \det(A) \epsilon\left(e_{j_1}, \dots, e_{j_n} \right)\\
&= \det(A) \epsilon\left(B_{j_1 1} e_{j_1}, \dots, B_{j_n n} e_{j_n} \right)\\
&= \det(A) \det(B),
\end{aligned}$$

where from the third to fourth line we used that

$$\begin{aligned}
\epsilon\left(A e_{j_1}, \dots, A e_{j_n} \right) &= \epsilon\left(A_{i_1, j_1} e_{i_1}, \dots, A_{i_n, j_n} e_{i_n}\right)\\
&= \epsilon\left(A_{j_1}, \dots, A_{j_n} \right)\\
&= \textrm{sgn}(\sigma) \epsilon\left(A_1, \dots, A_n \right)\\
&= \textrm{sgn}(\sigma) \det A.
\end{aligned}$$

Here we defined $$\sigma$$ to be the permutation that maps $$i \mapsto j_i$$; thus, 

$$\begin{aligned}
\textrm{sgn}(\sigma) &= \epsilon(e_{\sigma(1)}, \dots, e_{\sigma(n)})\\
&= \epsilon(e_{j_1}, \dots, e_{j_n}).
\end{aligned}$$

This proves our step from the third to the fourth line and therefore completes the proof. {% include endproof.html %}


**Property 2**: $$\det(A) = \det(A^T)$$.

*Proof*: Using the definition of determinant, we have

$$\begin{aligned}
\det A &= \sum_{\sigma \in S_n} \textrm{sgn}(\sigma) \prod_{i=1}^n A_{\sigma(i)i}\\
&= \sum_{\sigma \in S_n} \textrm{sgn}(\sigma) \prod_{i=1}^n A_{\sigma(\rho(i)) \rho(i)}\\
\end{aligned}$$

for any permutation $$\rho \in S_n$$. So let's choose $$\rho = \sigma^{-1}$$, then

$$\begin{aligned}
\det A &= \sum_{\sigma \in S_n} \textrm{sgn}(\sigma) \prod_{i=1}^n A_{\sigma(\rho(i)) \rho(i)}\\
&= \sum_{\sigma \in S_n} \textrm{sgn}(\sigma) \prod_{i=1}^n A_{i \sigma^{-1}(i)}\\
&= \sum_{\sigma' \in S_n} \textrm{sgn}(\sigma') \prod_{i=1}^n A_{i \sigma'(i)}\\
&= \sum_{\sigma' \in S_n} \textrm{sgn}(\sigma') \prod_{i=1}^n A^T_{\sigma'(i)i}\\
&= \det A^T,
\end{aligned}$$

where we used in the third line that $$\textrm{sgn}(\sigma) = \textrm{sgn}(\sigma^{-1})$$ for any permutation. {% include endproof.html %}


Recall that orthogonal and unitary transformations are used to go from one orthonormal basis to another orthonormal basis because they act as isometries.

$$\begin{aligned}
\delta_{ij} &= (e_i\vert e_j)\\
&= (A e_i \vert A e_j)\\
&= (e_i \vert A^* A e_j),
\end{aligned}$$

where $$A^*$$ is the adjoint of $$A$$. So for $$V = \mathbb R^n$$, $$A^T A = I$$, and for $$V = \mathbb C^n$$, $$A^\dagger A = I$$. 

**Property 3**: $$A$$ is an orthogonal or unitary matrix $$\Rightarrow \abs{\det (A)} = 1$$.

*Proof*: For the orthogonal case,

$$\begin{aligned}
1 &= \det(I)\\
&= \det(A A^T)\\
&= \det(A)\det(A^T)\\
&= \det(A) \det(A)\\
&= \det(A)^2,
\end{aligned}$$

where we used property 1 in the third line and property 2 in the fourth line. The analagous result works for the unitary case. {% include endproof.html %}

### Volume

Now we argue that the determinant is related to (signed) volume. Consider the unit $$n$$-cube defined by the volume enclosed by the unit vectors $$\{e_1, \dots, e_n \}$$. The volume of such a cube is 1, which happens to also be $$\epsilon(e_1, \dots, e_n) = 1$$. Now we consider a matrix $$A$$ that sends the orthonormal basis $$\{e_1, \dots, e_n\}$$ to a set $$\{A_{1}^j e_j, \dots, A_n^j e_j \}$$ (recall summation convension). Since a tensor is multilinear, we then have that

$$\begin{aligned}
\epsilon(A_{1}^{j_1} e_{j_1}, \dots, A_n^{j_n} e_{j_n}) &= A_1^{j_1} \dots A_n^{j_n} \epsilon(e_{j_1}, \dots, e_{j_{n}})\\
&= \sum_{\sigma\in S_n}A_1^{\sigma(1)} \dots A_n^{\sigma(n)} \epsilon(e_{\sigma(1)}, \dots, e_{\sigma(n)})\\
&= \sum_{\sigma\in S_n}A_1^{\sigma(1)} \dots A_n^{\sigma(n)} \textrm{sgn}(\sigma)\\
&= \det(A),
\end{aligned}$$

where we go from the first to second line by noting that any case in which $$j_i = j_k$$ for $$i \neq k$$ will result in a zero from $$\epsilon(e_{j_1}, \dots, e_{j_{n}})$$ - so we only have to consider permutations of $$1, \dots, n$$ instead of $$j_1, \dots, j_n = 1, \dots, n$$.

Consider the volume that is spanned by the new set of vectors $$\{v_1 \coloneqq A_{1}^j e_j, \dots, v_n \coloneqq A_n^j e_j \}$$. We apply the Gram-Schmidt procedure to this set to get that

$$\begin{aligned}
v_1 &= v_1\\
v_2 &= \alpha_{12}v_1 + v_2^\perp\\
v_3 &= \alpha_{13}v_1 + \alpha_{23}v_2 + v_3^\perp\\
&~~~\vdots
\end{aligned}$$

for some constants $$\alpha_{ij}$$, where recall $$v_2^\perp$$ is perpendicular to $$v_1$$, $$v_3^\perp$$ is perpendicular to $$v_1$$ and $$v_2$$, and so on. Using the multilinearity and antisymmetry of $$\epsilon$$ then, we have that

$$\begin{aligned}
\epsilon(v_1, v_2, v_3, \dots, v_n) &= \epsilon(v_1, \alpha_{12} v_1 + v_2^\perp, \alpha_{13}v_1 + \alpha_{23}v_2 + v_3^\perp, \dots)\\
&= \epsilon(v_1, v_2^\perp, v_3^\perp, \dots, v_n^\perp)
\end{aligned}$$

since, for example, something like $$\epsilon(v_1, v_1, \dots) = 0$$ due to antisymmetry. Since these are all orthogonal, we can define a new orthonormal basis $$\{f_i \}$$ such that 

$$\begin{aligned}
v_1 &= \norm{v_1} f_1\\
v_2 &= \norm{v_2^\perp} f_2\\
v_3 &= \norm{v_3^\perp} f_3\\
&~~\vdots
\end{aligned}$$

Then

$$\epsilon(v_1, v_2, v_3, \dots, v_n) = \norm{v_1} \cdot \norm{v_2^\perp} \cdot \norm{v_3^\perp} \dots \cdot \epsilon(f_1, \dots, f_n).$$

Since $$\{f_i \}$$ is orthonormal, we know that $$\{ e_i\}$$ and $$\{f_i\}$$ are related by some orthogonal/unitary transformation $$T$$. We also showed above that for a change of basis tranformation $$T$$, $$\epsilon(Te_1, \dots, Te_n) = \det(T)$$. In this case, $$T$$ is orthogonal/unitary, and so as we showed in Property 3 has determinant equal to $$\pm 1$$. Thus,

$$\epsilon(v_1, v_2, v_3, \dots, v_n) = \pm \norm{v_1} \cdot \norm{v_2^\perp} \cdot \norm{v_3^\perp} \dots$$

where the sign depends on the transformation from the $$\{e_i\}$$ basis to the $$\{f_i\}$$ basis. We easily now recognize $$\norm{v_1} \cdot \norm{v_2^\perp} \cdot \norm{v_3^\perp} \dots$$ as the volume enclosed by the vectors $$v_1, \dots, v_n$$.

In the case of the determinant, $$v_1, \dots, v_n$$ represent the columns of the matrix in question. So the determinant gives the (signed) volume enclosed by the column vectors of the matrix. Going back to the beginning now, we found that 

$$\epsilon(A_{1}^{j_1} e_{j_1}, \dots, A_n^{j_n} e_{j_n}) = \det(A),$$

where $$\{A_{i}^j e_j\}$$ is the transformation of the orthonormal basis $$\{e_i \}$$ given by $$A$$. We now see that this is just the (signed) volume enclosed by the new set of vectors. Hence, the determinant tells us how much a transformation on a set of vectors will affect the resulting volume enclosed by the vectors.

### Jacobian

So we have seen that for a change of basis matrix A $$e_{i'} = A^{j}_{i'} e_j$$, the ratio of the volume spanned by $$\{e_{i'} \}$$ and the volume spanned by $$\{e_i \}$$ is $$\vert \det(A) \vert$$. Consider performing a volume integral with $$dV = \prod_i dx_i$$. When we transform coordinates with $$dx_i' = \frac{\partial x_i'}{\partial x_j} dx_j$$, the proportional change in volume is thus $$\left\lvert\det J \right\rvert$$, where $$J_{ij} \coloneqq \frac{\partial x_i'}{\partial x_j}$$ is the Jacobian matrix. Therefore, to componsate for the change so that $$dV$$ remains the same, we have that $$dV = \left\lvert\det J \right\rvert^{-1} \prod_{i'} dx_{i}'$$.

So, for example, when switching from cartesian coordinates $$x, y$$ to polar coordinates $$r, \theta$$ in an area integral, we have that

$$\begin{aligned}
dA &= dx dy\\
&= \left\lvert \det\left(\begin{matrix}\frac{\partial r}{\partial x}&\frac{\partial r}{\partial y}\\ \frac{\partial \theta}{\partial x}&\frac{\partial \theta}{\partial y} \end{matrix} \right)\right\rvert^{-1} dr d\theta\\
&= \left\lvert \frac{\partial r}{\partial x}\cdot \frac{\partial \theta}{\partial y} - \frac{\partial r}{\partial y} \cdot \frac{\partial \theta}{\partial x} \right\rvert^{-1} dr d\theta\\
&= \left\lvert \cos\theta\cdot \left(\cos\theta/r \right) - \sin\theta \cdot \left(-\sin\theta/r \right) \right\rvert^{-1} dr d\theta\\
&= r dr d\theta
\end{aligned}$$

where we computed the partial derivates via the relations

$$\begin{aligned}
r &= \sqrt{x^2 + y^2},\\
\theta &= \tan^{-1}(y/x).
\end{aligned}$$


### A note on the permanent

We remark here that Property 1 can be easily applied to show that $$\det(A)$$ is independent of the basis that $$A$$ is defined with respect to. Consider a change of basis matrix $$T$$, so that $$A' = T A T^{-1}$$ (where $$A'$$ is the matrix of $$A$$ represented in the different basis). Then, using Property 1,

$$\begin{aligned}
\det(A') &= \det(T A T^{-1})\\
&= \det(T)\det(A)\det(T^{-1})\\
&= \det(T T^{-1})\det(A)\\
&= \det(A).
\end{aligned}$$

This implies that the determinant is really a quantity of the operator itself, as opposed to its matrix representation. On the other hand, the permanent of $$A$$, $$\textrm{perm}(A)$$, is *not* basis independent, and so is a quantity of the matrix as opposed to the operator. The permanent is defined similarly to the determinant, but without any permutation signs;

$$\textrm{perm}(A) \coloneqq \sum_{\sigma\in S_n}\prod_{i=1}^n A_{\sigma(i)i}.$$

We can give a simple example of where the permanent is basis dependent. Consider the matrix

$$Z = \left(\begin{matrix}1&0\\0&-1 \end{matrix}\right)$$

and the matrix

$$X = \left(\begin{matrix}0&1\\1&0 \end{matrix}\right).$$

These are related by the change of basis

$$H = \frac{1}{\sqrt{2}}\left(\begin{matrix} 1&1\\1&-1 \end{matrix}\right),$$

so that $$X = H Z H^{-1}$$. We see that

$$\textrm{perm}(Z) = -1 \neq \textrm{perm}(X) = 1,$$

showing that the permanent is dependent on the basis representation.


{% include post-footer.html %}
