---
title: The connection between bosons and the permanent
comments: 19
---

{% include post-header.md %}

(07 May 2021) In this post, I will derive the relationship between bosons and the matrix permanent. This ultimately serves as the basis for the argument that BosonSampling is computationally hard, since computing the matrix permanent is known to be <span style="font-variant: small-caps;">#P-Hard</span>. I will take a different approach than was taken in the [BosonSampling paper](https://www.theoryofcomputing.org/articles/v009a004/v009a004.pdf). I have [another post](bosonsampling-formalism.html) that moreso follows along with the paper. But I personally prefer this way.

**Contents:**

* TOC
{:toc}


## Formalism

The following is partially motivated by [these notes](http://math.univ-lyon1.fr/~attal/Mescours/fock.pdf). Please note that $[n] \coloneqq \set{1, 2, \dots, n}$ is the set of positive integers less than or equal to $n$.


### Single boson states

We will consider a system of $m$ *modes*. In the case of photons, optical modes are orthogonal solutions to the equations of motion for the propagation of electromagnetic waves given a set of boundary conditions. For the BosonSampling formalism, we can simply view a system of modes as an a physical layout of waveguides; the photon can live in any superposition of the $m$ waveguides.

Mathematically, the boson lives in the Hilbert space $H_{m, 1} \coloneqq \bbC^m$. Thus, for a single boson system, the modes form a direct product space. We will choose the orthonormal basis of $H_{m,1}$ $\calB_{m,1} \coloneqq \set{e_i\mid i\in [m]}$, where each basis vector is

\begin{equation}
    e\_i \coloneqq 
    \begin{pmatrix}
      \bm 0\_{i-1}\\\\\\\\
      1\\\\\\\\
      \bm 0\_{m-i}
    \end{pmatrix} = \parentheses{\bigoplus\_{j=1}^{i-1} 0} \oplus 1 \oplus \parentheses{\bigoplus\_{j=1}^{m-i} 0}.
\end{equation}

There are three operations that a linear-optical network can perform on the two-dimensional Hilbert space $H_{2,1}$. The first and second are phase shifts on the first and second modes, and the third is the beamsplitter;

\begin{equation}
    P_1(\phi) = e^{i\phi} \oplus 1, \quad P_2(\phi) = 1\oplus e^{i\phi}, \quad B(\theta) = 
    \begin{pmatrix}
      \cos \theta&-\sin\theta\\\\\\\\
      \sin\theta&\cos\theta
    \end{pmatrix}
\end{equation}

Here the direct sum is to be understood as the direct sum of operators, namely $a \oplus b = \text{diag}(a, b)$. Together, products of these three operations can generate an arbitrary unitary operation on $\bbC^2$.

**Example** *(The SWAP operation on $H_{2, 1}$)* The SWAP operation on $H_{2,1}$ is the involution that swaps the two modes, and is defined by its action on the two basis states

\begin{align}
    \text{SWAP}(e_1) &= e_2,\\\\\\\\
    \text{SWAP}(e_2) &= e_1.
\end{align}

Therefore, SWAP $ = P_1(\pi) \circ B(\pi/2) = \sigma^x$. {% include endproof.html %}

Now suppose we allow an arbitrary number of modes $m$, but still restrict to one photon. An arbitrary unitary operation on $H_{m,1}$ can be represented by a product of at most $\calO(m^2)$ unitary operations that act non-trivially on only one or two modes ([source](https://link.aps.org/doi/10.1103/PhysRevLett.73.58)). Using the SWAP operation between nearest-neighbor modes, SWAP networks can be generated so that beamsplitter gates need only be performed between nearest-neighbor modes (e.g. assuming a one-dimensional architecture). The SWAP networks could themselves require $\calO(m)$ SWAP gates between adjacent modes. As such, an arbitrary unitary operation on $H_{m,1}$ can be implemented by a sequence of $\calO(m^3)$ operations of the form

\begin{equation}
    \underbrace{1 \oplus \dots \oplus 1}\_{i} \oplus \parentheses{P\_1(\phi\_1)\circ P\_2(\phi\_2)\circ B(\theta)} \oplus \underbrace{1 \oplus \dots \oplus 1}\_{m-i-2}
\end{equation}

for any $0 \leq i \leq m-2$ and angles $\phi_1, \phi_2, \theta$.


### Many boson states

We've seen that an $m$-mode system of one boson is nothing more than an $m$-dimensional qudit system. However, bosonic systems become interesting when we introduce multiple particles. Clearly, a $2$-boson system will be in the Hilbert space $H_{m,1} \otimes H_{m,1}$. The state $e_1 \otimes e_2$, for example, represents the first boson being in the first mode and the second boson being in the second mode. Quantum field theory teaches that fundamental particles are indistinguishable. As such, labeling one boson as the *first* and the other as the *second* does not make any physical sense. In other words, the vector $e_1 \otimes e_2$ and $e_2 \otimes e_1$ represent the same quantum state of one boson in the first mode and one boson in the second mode. This suggest that we define an equivalence relation $\sim$ such that $e_1 \otimes e_2 \sim e_2 \otimes e_1$. In this way, there is no way to tell *which* boson is in which mode. Indeed, this is how we define bosons in the following definition.

**Definition** *(Bosons)* For $v_1,\dots, v_n \in H_{m,1}$, define the equivalence relation $\sim$ that satisfies $v_1 \otimes \dots \otimes v_n \sim v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)}$ for any $\pi \in S_n$. Then the quantum state of $n$ bosons lives in $H_{m,n} \coloneqq H_{m,1}^{\otimes n} /\mathord \sim$. {% include endproof.html %}

Note that this is equivalent to

\begin{equation}
    H_{m,n} = H_{m,1}^{\otimes n} / \mathord{\set{v_1\otimes \dots \otimes v_n - v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)} \mid v_i \in H_{m,1}, \pi\in S_n}}.
\end{equation}

**Example** *($H_{3, 2}$)* The space of two *distinguishable* three-level particles is

\begin{equation}
    H_{3,1}^{\otimes 2} = \text{span}\cbargs{e_i \otimes e_j \mid i, j \in [3]},
\end{equation}

where recall an orthonormal basis of $H_{3,1}$ is $\calB_{3,1} = \set{e_i\mid i\in [3]}$. We notice that $e_i \otimes e_j \sim e_j \otimes e_i$. Thus, the space of two three-level bosons is

\begin{equation}
    H_{3,2} = \text{span}\cbargs{\brackets{e_i \otimes e_j} \mid i \leq j \in [3]},
\end{equation}

where $\brackets{\cdot}$ denotes the equivalence class, so that

\begin{equation}
    \brackets{e_i \otimes e_j} = \set{e_i \otimes e_j + u \otimes v - v \otimes u \mid u, v \in H_{3,1}}.
\end{equation}

One natural set of representatives of the equivalence classes is the set

\begin{equation}
    \begin{aligned}
        &\set{e_1\otimes e_1, e_2 \otimes e_2, e_3 \otimes e_3} \\\\\\\\
         & \qquad \cup \set{\frac{1}{{2}} \parentheses{e_1 \otimes e_2 + e_2 \otimes e_1}, \frac{1}{{2}} \parentheses{e_1 \otimes e_3 + e_3 \otimes e_1}, \frac{1}{{2}} \parentheses{e_2 \otimes e_3 + e_3 \otimes e_2}},
    \end{aligned}
\end{equation}

where we note that, for example, $\brackets{e_1 \otimes e_2} = \brackets{\frac{1}{{2}} \parentheses{e_1 \otimes e_2 + e_2 \otimes e_1}}$. {% include endproof.html %}

As noted in the example, the most convenient set of representatives of the quotient space to work with is the set of all rank $n$ symmetric tensors on $H_{m,1}$. By choosing this set of representatives, the inner product induced from the space $H_{m,1}^{\otimes n}$ behaves nicely in the sense that we can essentially forget about the equivalence relation altogether. We could of course choose any set of representatives provided that we ensure the inner product is respecting the equivalence relation; in fact I will show an example in the appendix below titled [another way to deal with the quotient space](#appendix:-another-way-to-deal-with-the-quotient-space) where we work with just the equivalence classes themselves. To that end, we will now fix the space $H_{m,n}$ to be all symmetric representatives and drop the equivalence classes. We define the inner product $\angles{\cdot, \cdot}\_{H_{m,n}}$ to be the inner product of the symmetric tensor representatives on $H_{m,1}^{\otimes n}$. In the following, I will write $\angles{\cdot, \cdot}$ to denote $\angles{\cdot, \cdot}\_{H_{m,1}^{\otimes n}}$ for brevity.

We define the map $b\colon H_{m,1}^n \to H_{m,n}$ as

\begin{equation}
    \label{eq:basisstates}
    b(v_1, \dots, v_n) = \frac{1}{\sqrt{n!}}\sum_{\pi \in S_n} v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)}.
\end{equation}

Similarly, for any map $\sigma\colon [n]\to [m]$, define $b_\sigma \coloneqq b(e_{\sigma(1)}, \dots, e_{\sigma(n)})$. Then

\begin{equation}
    \calB_{m,n} \coloneqq \set{b_\sigma \mid \sigma \in [m]^{[n]} ~\text{monotonically increasing}}
\end{equation}

forms an orthogonal basis (*not* orthonormal) of $H_{m,n}$ (note that $[m]^{[n]}$ denotes the set of maps with domain $[n]$ and codomain $[m]$). The restriction to monotonically increasing $\sigma$ is simply to avoid overcounting, since for any $\pi \in S_n$, $b(v_1, \dots, v_n) = b(v_{\pi(1)}, \dots, v_{\pi(n)})$. Noticing that $\abs{\calB_{m,n}}$ is equivalent to the number of ways to put $n$ identical balls (i.e. bosons) into $m$ distinguishable bins (i.e. modes), we find that

\begin{equation}
    M \coloneqq \dim H_{m,n} = \binom{n+m-1}{n}.
\end{equation}

Thus, $H_{m,n} \cong \bbC^M$.

**Definition** *(Multiplicity function)* Let $f^{-1}[b] \subseteq A$ denote the preimage of $b \subseteq B$ under the map $f\colon A \to B$. For a map $\sigma\colon [n]\to [m]$, define its multiplicity function $\calM_\sigma\colon [m] \to \curlybrackets{0} \cup [n]$ by $j \mapsto \abs{\sigma^{-1}[\curlybrackets{j}]}$. In words, the multiplicity function indicates how many elements in the domain of $\sigma$ map to a particular value in the codomain of $\sigma$. As such, $\calM_\sigma(i)$ is the number of bosons in the $i^{\rm th}$ mode for the state $b_\sigma$. {% include endproof.html %}

**Example** *(Multiplicity function)*
Suppose $n = 3$, $m = 3$, and $\sigma\colon [n]\to[m]$ such that $\sigma(1) = \sigma(2) = 1$ and $\sigma(3) = 2$. The multiplicity function is $\calM_\sigma(1) = 2$, $\calM_\sigma(2) = 1$, and $\calM_\sigma(3) = 0$. Thus, $b_\sigma$ is the state with two bosons in the first mode, one boson in the second mode, and no bosons in the third mode, $b_\sigma = \frac{2}{\sqrt{3!}}\parentheses{e_1 \otimes e_1 \otimes e_2 + e_1 \otimes e_2 \otimes e_1 + e_2 \otimes e_1 \otimes e_1}.$ {% include endproof.html %}

Using the multiplicity function, we can now more easily understand the quantum state described by $b_\sigma$; namely, $b_\sigma$ describes the (unnormalized) state with $\calM_\sigma(i)$ bosons in mode $i \in [m]$. Since we are describing quantum states, we will eventually require that the states be normalized. We will then need the following lemma.

**Lemma:** *For any $\sigma\colon [n]\to [m]$, $\norm{b_\sigma}^2 \coloneqq \angles{b_\sigma, b_\sigma} = \prod_{i \in [m]} \calM_\sigma(i)!$.*

*Proof:* Starting from \eqref{eq:basisstates},

\begin{align}
    \angles{b_\sigma, b_\sigma} &= \frac{1}{n!}\sum_{\pi,\pi'\in S_n}\angles{e_{\sigma(\pi(1))} \otimes \dots \otimes e_{\sigma(\pi(n))}, e_{\sigma(\pi'(1))} \otimes \dots \otimes e_{\sigma(\pi'(n))}}\\\\\\\\
    &= \frac{1}{n!}\sum_{\pi,\pi'\in S_n} \prod_{i=1}^n \angles{e_{\sigma(\pi(i))}, e_{\sigma(\pi'(i))}}\\\\\\\\
    &= \sum_{\pi\in S_n} \prod_{i=1}^n \angles{e_{\sigma(\pi(i))}, e_{\sigma(i)}}.
\end{align}

This is equal to the number of permutations $\pi$ for which $\sigma(\pi(i)) = \sigma(i)$ for all $i$. Indeed we see that if $\sigma$ is injective, there must only be one such permutation. More generally, for each $j \in [m]$ for which there is only one $i \in [n]$ where $\sigma(i) = j$ (i.e. $\calM_\sigma(j)= 1$), $\pi$ must be the identity on $i$. For each $j \in [m]$ for which there are two $i_1, i_2 \in [n]$ such that $\sigma(i_1) = \sigma(i_2) = j$ (i.e. $\calM_\sigma(j)= 2$), $\pi$ can act as either the identity or the swap on the subset of inputs $\set{i_1, i_2}$. In general, whenever $\sigma(i_1) = \dots = \sigma(i_a) = j$ (i.e. $\calM_\sigma(j) = a$), $\pi$ can act as any permutation in $S_a$ on the subset $\set{i_1, \dots, i_a} \subset [n]$. Therefore, there are $\prod_{j=1}^m \calM_\sigma(j)!$ permutations $\pi \in S_n$ for which the product $\prod_{i=1}^n \angles{e_{\sigma(\pi(i))}, e_{\sigma(i)}}$ does not vanish. {% include endproof.html %}



### Relationship to the permanent

In the first section, we described unitary operations on a one boson $m$-mode system, where the unitary acts on the modes. In a similar way, we are interested in the way such a unitary acts on an $n$-boson system. Again, one should think of the unitary as acting on the modes, which then affects how the bosons distribute themselves throughout the modes. Thus, we extend the unitary on $H_{m,1}$ to $H_{m,n}$ via a homomorphism that acts symmetrically on the bosons.

**Definition** *($f \in \Hom{U(m), U(M)}$)* Given a single particle unitary $U \in \Aut{H_{m,1}}$, we extend it to an $n$ boson unitary $f(U) \in \Aut{H_{m,n}}$ by $f(U) = U^{\otimes n}$. {% include endproof.html %}

The action of $f(U)$ on the basis $\calB_{m,n}$ is then

\begin{align}
    \angles{b_\sigma, f(U)b_{\sigma'}} &= \angles{b(e_{\sigma(1)}, \dots, e_{\sigma(n)}), b(Ue_{\sigma'(1)}, \dots, Ue_{\sigma'(n)})}\\\\\\\\
    &= \frac{1}{n!}\sum_{\pi,\pi'\in S_n} \angles{e_{\sigma(\pi(1))} \otimes \dots \otimes e_{\sigma(\pi(n))}, Ue_{\sigma'(\pi'(1))} \otimes \dots \otimes Ue_{\sigma'(\pi'(n))}}\\\\\\\\
    &= \frac{1}{n!}\sum_{\pi,\pi'\in S_n} \prod_{i=1}^n \angles{e_{\sigma(\pi(i))}, Ue_{\sigma'(\pi'(i))}}\\\\\\\\
    &= \sum_{\pi\in S_n} \prod_{i=1}^n \angles{e_{\sigma(\pi(i))}, Ue_{\sigma'(i)}}.
\end{align}

Define $U(\sigma, \sigma')$ to be the $n \times n$ matrix with entries $U(\sigma,\sigma')\_{ij} = \angles{e\_{\sigma(i)}, U e\_{\sigma'(j)}}$. Thus, $U(\sigma, \sigma')$ is the matrix created from the matrix of $U$ in the basis $\calB_{m,1}$ as follows. For each row $r \in \Im{\sigma}$ of $U$, we repeat that row $\calM_{\sigma}(r)$ times. Then for each column $c \in \Im{\sigma'}$ of $U$, we repeat that column $\calM_{\sigma'}(c)$ times. By definition of the permanent for an $N \times N$ matrix,

\begin{equation}
    \label{eq:permanent}
    \perm(A) \coloneqq \sum_{\pi \in S_N} \prod_{i=1}^N A_{\pi(i),i},
\end{equation}

we have that

\begin{equation}
    \angles{b_\sigma, f(U)b_{\sigma'}} = \perm(U(\sigma, \sigma')).
\end{equation}

**Example** *($H_{3,2}$)* Consider $\sigma, \sigma'$ defined as $\sigma(1) = \sigma(2) = 3$ and $\sigma'(1)= 2$, $\sigma'(2) = 3$. Let $U$ be the $3 \times 3$ unitary matrix with entries $U_{ij}$. Then

\begin{equation}
    U(\sigma, \sigma') = \begin{pmatrix} 
      U_{3 2} & U_{3 3}\\\\\\\\
      U_{3 2} & U_{3 3}
    \end{pmatrix}.
\end{equation}

In this case, $b_\sigma = \sqrt{2}e_3 \otimes e_3$ and $b_{\sigma'} = \frac{1}{\sqrt{2}}\parentheses{e_2 \otimes e_3 + e_3 \otimes e_2}$, and $\perm(U(\sigma, \sigma')) = 2U_{32}U_{33}$. {% include endproof.html %}

Putting this together with the lemma, we find that the probability to measure the normalized basis state $b_{\sigma} / \norm{b_\sigma}$ after applying the unitary $f(U)$ to the normalized basis state $b_{\sigma'} / \norm{b_{\sigma'}}$ is

\begin{equation}
    \label{eq:BSEquationSigma}
    \Pr[\sigma' \xrightarrow{U} \sigma] \coloneqq \frac{\abs{\angles{b_\sigma, f(U)b_{\sigma'}}}^2}{\norm{b_\sigma}^2 \norm{b_{\sigma'}}^2} = \frac{\abs{\perm(U(\sigma,\sigma'))}^2}{\prod_{i=1}^m \calM_\sigma(i)! \cdot \calM_{\sigma'}(i)!}
\end{equation}

As noted previously, $b_\sigma$ represents the unnormalized quantum state with $\calM_\sigma(i)$ bosons in mode $i \in [m]$. We can thus define $\ket{\bm n}$ to be $b_\sigma / \norm{b_\sigma}$, where $\bm n \in \bbN_0^m$ satisfies $n_i = \calM_\sigma(i)$ (note that $\bbN_0$ denotes the set of natural numbers including $0$). In this case, the so called Fock orthonormal basis is $\set{\ket{\bm n} \mid \bm n \in \Phi_{m,n}}$ where

\begin{equation}
    \Phi_{m,n} \coloneqq \set{\bm n \in \bbN_0^m ~\big\vert~ \sum_{i=1}^m n_i = n}.
\end{equation}

Since there is a one-to-one correspondence between $\bm n$ and $\sigma$, we can rewrite \eqref{eq:BSEquationSigma} as

\begin{equation}
    \label{eq:BSEquation}
    \Pr[\bm n' \xrightarrow{U} \bm n] = \frac{\abs{\perm(U(\bm n, \bm n'))}^2}{\prod_{i=1}^m n_i! \cdot n_i'!},
\end{equation}

where $U(\bm n, \bm n')$ is the $n \times n$ matrix gotten from $U$ by repeating each row $r \in [m]$ $n_r$ times and each column $c \in [m]$ $n_c'$ times.



## Variants of the formalism

Here we will discuss what happens when the bosons are replaced with distinguishable particles (e.g. billiard balls), or with fermions.


### Distinguishable particles

In [Many boson states](#many-boson-states), we defined bosons by the equivalence relation $\sim$ that satisfied $v_1 \otimes \dots \otimes v_n \sim v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)}$ for any $\pi \in S_n$. This was motivated by the fact that bosons are indistinguishable. Thus, the space of $n$ bosons was $H_{m,1}^{\otimes n} / \mathord \sim$. In the "classical" case, particles are distinguishable, and so no such equivalence relation exists. In this case, the space is simply $H_{m,1}^{\otimes n}$. Our homomorphsim $f \in \Hom{U(m), U(m^n)}$ is still $f(U) = U^{\otimes n}$. The transition probability from $e_{\sigma'(1)} \otimes \dots \otimes e_{\sigma'(n)}$ to $e_{\sigma(1)} \otimes \dots \otimes e_{\sigma(n)}$ (where now $\sigma, \sigma'$ do not need to be monotonically increasing) is

\begin{align}
    \abs{\angles{e_{\sigma(1)} \otimes \dots \otimes e_{\sigma(n)}, f(U)e_{\sigma'(1)} \otimes \dots \otimes e_{\sigma'(n)}}}^2 &= \prod_{i=1}^n \abs{\angles{e_{\sigma(i)}, U e_{\sigma'(i)}}}^2\\\\\\\\
    &= \prod_{i=1}^n \abs{U_{\sigma(i) \sigma'(i)}}^2.
\end{align}

In analogy to the case with bosons, we are interested in the transition probability to a state with one particle in mode $\sigma(1)$, one particle in mode $\sigma(2)$, and so forth. This probability is then

\begin{align}
    \sum_{\pi \in S_n} \abs{\angles{e_{\sigma(\pi(1))} \otimes \dots \otimes e_{\sigma(\pi(n))}, f(U)e_{\sigma'(1)} \otimes \dots \otimes e_{\sigma'(n)}}}^2 &= \sum_{\pi \in S_n}\prod_{i=1}^n \abs{U_{\sigma(\pi(i)) \sigma'(i)}}^2\\\\\\\\
    &= \perm\pargs{\abs{U(\sigma, \sigma')}^2}
\end{align}

where the absolute value and the square are elementwise. In comparing this to \eqref{eq:BSEquationSigma}, we see that the main difference (other than the denominator) is the location of the absolute value and square. As it turns out, approximating the permanent of a matrix with all nonnegative entries (such as $\abs{U(\sigma, \sigma')}^2$) up to multiplicative eror can be dones efficiently ([source](https://doi.org/10.1145/1008731.1008738)), whereas this is not the case for a general matrix (such as $U(\sigma, \sigma')$). Thus, computing the output probabilities for bosons is hard, while computing the output probabilities for classical distingushable particles is easy.


### Fermions

In [Many boson states](#many-boson-states), we defined bosons by the equivalence relation $\sim$ that satisfied $v_1 \otimes \dots \otimes v_n \sim v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)}$ for any $\pi \in S_n$. This was motivated by the fact that bosons are indistinguishable. Thus, the space of $n$ bosons was $H_{m,1}^{\otimes n} / \mathord \sim$. Since an overall phase factor doesn't affect a quantum state, there is another way for particles to be indistiguishable; namely, exchanging any two particles affects the quantum state by an overall minus sign. Such particles are called fermions.

**Definition** *(Fermions)* For $v_1,\dots, v_n \in H_{m,1}$, define the equivalence relation $\sim$ that satisfies $v_1 \otimes \dots \otimes v_n \sim \sgn{\pi} v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)}$ for any $\pi \in S_n$. Then the quantum state of $n$ fermions lives in $H_{m,1}^{\otimes n} /\mathord \sim$. {% include endproof.html %}

Note that this is equivalent to

\begin{equation}
     H_{m,1}^{\otimes n} / \mathord{\set{v_1\otimes \dots \otimes v_n - \sgn{\pi} v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)} \mid v_i \in H_{m,1}, \pi\in S_n}}.
\end{equation}

In this case, the simplest complete set of representatives is the set of antisymmetric tensors of rank $n$ on $H_{m,1}$. The analogue to \eqref{eq:basisstates} is then

\begin{equation}
    b(v_1, \dots, v_n) = \frac{1}{\sqrt{n!}}\sum_{\pi\in S_n} \sgn{\pi} v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)}.
\end{equation}

The basis is then

\begin{equation}
    \calB = \set{b_\sigma \mid \sigma \in [m]^{[n]} ~\text{monotonically increasing and injective}},
\end{equation}

where $b_\sigma = b(e_{\sigma(1)}, \dots, e_{\sigma(n)})$. The restriction to injective $\sigma$ is because $b_\sigma = 0$ for any non-injective $\sigma$. It's not hard to see that each $b_{\sigma}$ is already normalized, and thus $\calB$ is an orthonormal basis. So we get that

\begin{align}
    \angles{b_\sigma, f(U) b_{\sigma'}} &= \frac{1}{n!}\sum_{\pi,\pi' \in S_n} \sgn{\pi}\sgn{\pi'}\prod_{i=1}^n \angles{e_{\sigma(\pi(i))}, U e_{\sigma'(\pi'(i))}}\\\\\\\\
    &= \frac{1}{n!}\sum_{\pi,\pi' \in S_n} \sgn{\pi}\sgn{\pi'}\prod_{i=1}^n \angles{e_{\sigma(\pi(\pi^{' -1}(i)))}, U e_{\sigma'(i)}}\\\\\\\\
	&= \frac{1}{n!}\sum_{\pi,\pi' \in S_n} \sgn{\pi \circ \pi'}\prod_{i=1}^n \angles{e_{\sigma(\pi \circ \pi^{' -1}(i))}, U e_{\sigma'(i)}}\\\\\\\\
	&= \frac{1}{n!}\sum_{\rho,\pi' \in S_n} \sgn{\rho}\prod_{i=1}^n \angles{e_{\sigma(\rho(i))}, U e_{\sigma'(i)}}\\\\\\\\
	&= \sum_{\rho\in S_n} \sgn{\rho}\prod_{i=1}^n \angles{e_{\sigma(\rho(i))}, U e_{\sigma'(i)}}\\\\\\\\
	&= \sum_{\rho\in S_n} \sgn{\rho}\prod_{i=1}^n U_{\sigma(\rho(i)), \sigma'(i)}\\\\\\\\
	&= \det\pargs{U(\sigma, \sigma')}.
\end{align}

Thus, we see that while for bosons we get the permanent, for fermions we get the determinent. The permanent is hard to compute (takes exponential time), but the determinent is easy (takes polynomial time) by computing the $LU$ decomposition of $U(\sigma, \sigma')$ and then using that $\det(LU) = \det(L)\det(U)$. Therefore, computing the output probabilities in the case of fermions is easy.


## Appendix: another way to deal with the quotient space

In [Many boson states](#many-boson-states), we defined bosons by the equivalence relation $\sim$ that satisfied $v_1 \otimes \dots \otimes v_n \sim v_{\pi(1)} \otimes \dots \otimes v_{\pi(n)}$ for any $\pi \in S_n$. This was motivated by the fact that bosons are indistinguishable. Thus, the space of $n$ bosons was $H_{m,n} = H_{m,1}^{\otimes n} / \mathord \sim$. We then redefined $H_{m,n}$ by using a complete set of representatives of the equivalence classes, those being the symmetric tensor representatives. In this section, I will illustrate that we could have chosen any set of representatives with a suitable choice of an inner product. I will select representatives so that a orthogonal basis is

\begin{equation}
    \calB = \set{e_{\sigma(1)} \otimes \dots \otimes e_{\sigma(n)} \mid \sigma\in [m]^{[n]} ~\text{monotonically increasing}}.
\end{equation}

In this case, though, we will have to redefine our inner product because $f(U)$ is not unitary with respect to the naive inner product. For example, in the $n=2$ case, if we stick with the naive inner product and assume that $f(U)$ *is* unitary, then

\begin{align}
    1 &= \angles{e_1 \otimes e_1, e_1 \otimes e_1}\\\\\\\\
    &= \angles{f(U) e_1 \otimes e_1, f(U) e_1 \otimes e_1}\\\\\\\\
    &= \angles{\parentheses{U_{11}e_1 + U_{21} e_2} \otimes \parentheses{U_{11}e_1 + U_{21} e_2}, \parentheses{U_{11}e_1 + U_{21} e_2} \otimes \parentheses{U_{11}e_1 + U_{21} e_2}}\\\\\\\\
    &= \big\langle U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + U_{11}U_{21} \parentheses{e_1 \otimes e_2 + e_2 \otimes e_1},\\\\\\\\
    &\qquad U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + U_{11}U_{21} \parentheses{e_1 \otimes e_2 + e_2 \otimes e_1} \big\rangle \nonumber \\\\\\\\
    &\sim \big\langle U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + 2U_{11}U_{21} e_1 \otimes e_2,\\\\\\\\
    &\qquad U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + 2U_{11}U_{21} e_1 \otimes e_2 \big\rangle\nonumber \\\\\\\\
    &= \abs{U_{11}}^4 + \abs{U_{21}}^4 + 4 \abs{U_{11}U_{21}}^2\\\\\\\\
    &\neq 1.
\end{align}

Notice that this is not equal to one for a general $2 \times 2$ unitary matrix. If the $4$ in front of $\abs{U_{11}U_{21}}^2$ was a $2$, then it actually would be equal to one. Indeed, the way to rectify this is to define the inner product such that $\angles{e_i \otimes e_i, e_i \otimes e_i} = 2$ and $\angles{e_1 \otimes e_2, e_1 \otimes e_2} = 1$. Then,

\begin{align}
    2 &= \angles{e_1 \otimes e_1, e_1 \otimes e_1}\\\\\\\\
    &= \angles{f(U) e_1 \otimes e_1, f(U) e_1 \otimes e_1}\\\\\\\\
    &= \angles{\parentheses{U_{11}e_1 + U_{21} e_2} \otimes \parentheses{U_{11}e_1 + U_{21} e_2}, \parentheses{U_{11}e_1 + U_{21} e_2} \otimes \parentheses{U_{11}e_1 + U_{21} e_2}}\\\\\\\\
    &= \big\langle U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + U_{11}U_{21} \parentheses{e_1 \otimes e_2 + e_2 \otimes e_1}, \\\\\\\\
    &\qquad U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + U_{11}U_{21} \parentheses{e_1 \otimes e_2 + e_2 \otimes e_1} \big\rangle \nonumber \\\\\\\\
    &\sim \big\langle U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + 2U_{11}U_{21} e_1 \otimes e_2, \\\\\\\\
    &\qquad U_{11}^2 e_1 \otimes e_1 + U_{21}^2 e_2 \otimes e_2 + 2U_{11}U_{21} e_1 \otimes e_2 \big\rangle \nonumber \\\\\\\\
    &= 2\abs{U_{11}}^4 + 2\abs{U_{21}}^4 + 4 \abs{U_{11}U_{21}}^2\\\\\\\\
    &= 2 \parentheses{\abs{U_{11}}^4 + \abs{U_{21}}^4 + 2 \abs{U_{11}U_{21}}^2}\\\\\\\\
    &= 2 \parentheses{\abs{U_{11}}^2 + \abs{U_{21}}^2}^2\\\\\\\\
    &= 1
\end{align}

because the columns of a unitary matrix are normalized to one. We generalize this in the case of arbitrary $n$. We define the inner product such that

\begin{equation}
    \norm{e_{\sigma(1)} \otimes \dots \otimes e_{\sigma(n)}}^2 = \angles{e_{\sigma(1)} \otimes \dots \otimes e_{\sigma(n)}, e_{\sigma(1)} \otimes \dots \otimes e_{\sigma(n)}} = \prod_{j=1}^m \calM_\sigma(j)!.
\end{equation}

With respect to this inner product, $f(U)$ is unitary. Indeed, from this one will reproduce \eqref{eq:BSEquationSigma} if they go through it. I will not go through the explicit calculation as I don't think it particularly instructive to go any further than this. The key point is that once you have defined your inner product in this way, then $f(U)$ is unitary. When calculating the inner product, you need to use the equivalence relation as we did above to replace vector that is "out of order" with one that is "in order". For example, if you compute $f(U)e_{1} \otimes e_{2} \otimes \dots$, you will end up with terms such as $e_{2}\otimes e_1 \otimes \dots$. You need to use the equivalence relation $\sim$ and replace it with $e_{1}\otimes e_2 \otimes \dots$.



{% include post-footer.html %}
