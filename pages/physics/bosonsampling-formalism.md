---
title: BosonSampling formalism
comments: 18
---

{% include post-header.md %}

(03 May 2021) In this post, I will derive the connection between bosons and the permanent in two ways - first, by following along with the [original BosonSampling paper][BS2013] (though I found their derivation of the permanent a bit confusing, so I will deviate slightly), and second, using linear-optics. Neither of these are my favorite way to derive the connection, but it was nonetheless instructive going through and understanding them. See [this post of mine](the-connection-between-bosons-and-the-permanent.md) for my preferred way of understanding the connection between bosons and the permanent.


**Contents**
1. [Aaronson & Arkhipov formulation](#aaronson--arkhipov-formulation)
   1. [Unitary operations on one photon](#unitary-operations-on-one-photon)
   2. [Unitary operations on many photons](#unitary-operations-on-many-photons)
   3. [Relationship to the permanent](#relationship-to-the-permanent)
2. [Linear optics formulation](#linear-optics-formulation)



## Aaronson & Arkhipov formulation

In this section, I will review BosonSampling as it is introduced in the [original paper][BS2013].
We begin with a quantum system of a fixed number $n$ of photons. Since photons are bosons, they are identical. The photons pass through a linear-optic network consisting of $m \geq n$ modes. Roughly speaking, optical modes are orthogonal solutions to the equations of motion for the propagation of electromagnetic waves given a set of boundary conditions. The relevant computational basis is the Fock (or occupation number) basis $\set{\ket{\bm n}\mid \bm n \in \Phi_{m,n}}$, where

\begin{equation}
    \Phi_{m,n} \coloneqq \set{\bm n \in \bbN_0^m ~\big\vert~ \sum_{i=1}^m n_i = n}.
\end{equation}

Here, $\bbN_0$ is the set of natural numbers including 0.
Noticing that $\abs{\Phi_{m,n}}$ is equivalent to the number of ways to put $n$ identical balls (i.e. photons) into $m$ distinguishable bins (i.e. modes), we find that

\begin{equation}
    M \coloneqq \abs{\Phi_{m,n}} = \binom{m+n-1}{n}.
\end{equation}

Thus, the quantum state of a BosonSampling computer lives in the Hilbert Space $H_{m,n}\coloneqq \bbC^M$.

Restricting our attention to $H_{m,1} = \bbC^m$, we note that it is not a tensor product space. An arbitrary unit vector in $H_{m,1}$ can be written as 

\begin{equation}
\sum_{i=1}^m \alpha\_i \lvert \underbrace{0\dots 0}\_{i-1} 1 \underbrace{0\dots 0}\_{m-i}\rangle.
\end{equation}

We can identify 

\begin{equation}
    \lvert \underbrace{0\dots 0}\_{i-1} 1 \underbrace{0\dots 0}\_{m-i}\rangle \longleftrightarrow 
    \begin{pmatrix}
    \bm 0\_{i-1}\\\\\\\\
    1\\\\\\\\
    \bm 0\_{m-i}
    \end{pmatrix} = \parentheses{\bigoplus\_{j=1}^{i-1} 0} \oplus 1 \oplus \parentheses{\bigoplus\_{j=1}^{m-i} 0}.
\end{equation}

Here the direct sum is to be understood as the direct sum of vectors.



### Unitary operations on one photon

There are three operations that a linear-optics network can perform on the two-dimensional Hilbert space $H_{2,1}$. The first and second are phase shifts on the first and second modes,

\begin{align}
    P_1(\phi) &= e^{i\phi} \oplus 1,\\\\\\\\
    P_2(\phi) &= 1\oplus e^{i\phi}.
\end{align}

Here the direct sum is to be understood as the direct sum of operators, namely $a \oplus b = \text{diag}(a, b)$. The third unitary operation is the *beamsplitter*,

\begin{equation}
    B(\theta) = \begin{pmatrix}
    \cos \theta&-\sin\theta\\\\\\\\
    \sin\theta&\cos\theta
    \end{pmatrix}.
\end{equation}

Together, products of these three operations can generate an arbitrary unitary operation on $\bbC^2$.

**Example** *(The SWAP operation on $H_{2, 1}$):*
The SWAP operation on $H_{2,1}$ swaps the two modes, and is defined by its action on the two basis states

\begin{align}
    \text{SWAP}\ket{1,0} &= \ket{0,1},\\\\\\\\
    \text{SWAP}\ket{0,1} &= \ket{1,0}.
\end{align}

Therefore, SWAP $ = P_1(\pi) \circ B(\pi/2)$. {% include endproof.html %}

Now suppose we allow an arbitrary number of modes $m$, but still restrict to one photon. An arbitrary unitary operation on $H_{m,1}$ can be represented by a product of at most $\calO(m^2)$ unitary operations that act non-trivially on only one or two modes ([source][DecompOfLinearOpticUnitary]). Using the SWAP operation between nearest-neighbor modes, SWAP networks can be generated so that beamsplitter gates need only be performed between nearest-neighbor modes (e.g. assuming a one-dimensional architecture). The SWAP networks could themselves require $\calO(m)$ SWAP gates between adjacent modes. As such, an arbitrary unitary operation on $H_{m,1}$ can be implemented by a sequence of $\calO(m^3)$ operations of the form

\begin{equation}
    \underbrace{1 \oplus \dots \oplus 1}\_{i} \oplus \parentheses{P\_1(\phi\_1)\circ P\_2(\phi\_2)\circ B(\theta)} \oplus \underbrace{1 \oplus \dots \oplus 1}\_{m-i-2}
\end{equation}

for any $0 \leq i \leq m-2$ and angles $\phi_1, \phi_2, \theta$.


### Unitary operations on many photons

Recall that $\dim H_{m,n} \eqqcolon M = \binom{m+n-1}{n}$. We would like to extend the $m\times m$ one photon unitaries on $H_{m,1}$ from the previous section to $M\times M$ unitaries on $H_{m,n}$. Thus, we now look for a homomorphism between the unitary group on $\bbC^m$ and the unitary group on $\bbC^M$, $f \in \Hom{U(m), U(M)}$. To do so, it is most convenient to represent the Fock states as polynomials of formal variables $x_i$. We use the computational basis state mapping

\begin{equation}
    \label{eq:monomial-def}
    \ket{\bm n} = \ket{n_1\dots n_m} \longleftrightarrow \prod_{i=1}^m \frac{x_i^{n_i}}{\sqrt{n_i!}}.
\end{equation}

The $\sqrt{n_i!}$ are needed because of the $n_i!$ possible permutations of the $x_i$ in $x_i^{n_i}$ that leave the term itself unchanged. Ultimately, they are necessary to ensure that $f(U)$ as defined next is unitary, which will be shown in soon. In the [last section of this post](#linear-optics-formulation), I will show that the factorials arise from the normalization when creating Fock states with creation operators. In fact, the formal variable $x_i$ is precisely the creation operator $a_i^\dagger$ on mode $i$.

With this mapping, a $2 \times 2$ unitary transformation $U$ between modes $i$ and $j$ acts on the basis as

\begin{equation}
    \label{eq:f}
    f(U)\parentheses{\frac{x_i^{n_i} x_j^{n_j}}{\sqrt{n_i! n_j!}}} \coloneqq \frac{1}{\sqrt{n_i! n_j!}}(U_{11}x_i + U_{21}x_j)^{n_i}(U_{12} x_i + U_{22} x_j)^{n_j}.
\end{equation}


**Example** *(Unitaries on polynomials):*
A unitary $U \in \Aut{H_{2,1}}$ acts as

\begin{align}
    U(x_1) = U_{11}x_1 + U_{21}x_2 ~\longleftrightarrow~U\ket{10} &= U_{11}\ket{10} + U_{21}\ket{01},\\\\\\\\
    U(x_2) = U_{12}x_1 + U_{22}x_2 ~\longleftrightarrow~U\ket{01} &= U_{12}\ket{10} + U_{22}\ket{01}.
\end{align}

Then with the homomorphism $f$, a unitary $U \in \Aut{H_{2,2}}$ acts as

\begin{align}
    &f(U)\parentheses{\frac{x_1^2}{\sqrt{2!}}} = \frac{1}{\sqrt{2!}}(U_{11}x_1 + U_{21}x_2)^2\\\\\\\\
    &~\longleftrightarrow~ f(U)\ket{20} = U_{11}^2 \ket{20} + \sqrt{2} U_{11}U_{21}\ket{11} + U_{21}^2\ket{02},\nonumber\\\\\\\\
    &f(U)(x_1 x_2) = (U_{11}x_1 + U_{21}x_2)(U_{12} x_1 + U_{22}x_2)\label{eq:f-example}\\\\\\\\
    &~\longleftrightarrow~ f(U)\ket{11} = \sqrt{2} U_{11}U_{12} \ket{20} + (U_{11}U_{22}+U_{12}U_{21})\ket{11} + \sqrt{2} U_{21}U_{22}\ket{02},\nonumber\\\\\\\\
    &f(U)\parentheses{\frac{x_2^2}{\sqrt{2!}}} = \frac{1}{\sqrt{2!}}(U_{12}x_1 + U_{22}x_2)^2\\\\\\\\
    &~\longleftrightarrow~ f(U)\ket{02} = U_{12}^2 \ket{20} + \sqrt{2} U_{12}U_{22}\ket{11} + U_{22}^2\ket{02}.\nonumber
\end{align}

This was a simple but instructive example. {% include endproof.html %}


**Theorem:** $f$ as defined in \eqref{eq:f} is a homomorphism.

*Proof:* By linearity, we can restrict our attention to a basis state $\prod_{i=1}^m x_i^{n_i}$. We can also restrict our attention to $2 \times 2$ unitary matrices $U$, since any $m\times m$ unitary can be built from them. Therefore, we must determine the action of $f(U)$ on $x_i^a x_j^b$ when $U$ acts between modes $i$ and $j$. Consider two such unitary matrices $U$ and $V$. Then,

\begin{align}
    f(U)\circ f(V) \parentheses{x_i^a x_j^b} &= f(U)\parentheses{\parentheses{V_{11}x_i + V_{21}x_j}^a \parentheses{V_{12}x_i + V_{22}x_j}^b}\\\\\\\\
    &= \parentheses{V_{11}\parentheses{U_{11}x_i + U_{21}x_j} + V_{21}\parentheses{U_{12}x_i + U_{22}x_j}}^a\\\\\\\\
    &\qquad \parentheses{V_{12}\parentheses{U_{11}x_i + U_{21}x_j} + V_{22}\parentheses{U_{12}x_i + U_{22}x_j}}^b\nonumber\\\\\\\\
    &= \parentheses{\parentheses{V_{11}U_{11}+V_{21}U_{12}}x_i + \parentheses{V_{11}U_{21} + V_{21}U_{22}}x_j}^a\\\\\\\\
    &\qquad \parentheses{\parentheses{V_{12}U_{11} + V_{22}U_{12}}x_i + \parentheses{V_{12}U_{21} + V_{22}U_{22}}x_j}^b\nonumber\\\\\\\\
    &= f\pargs{\begin{pmatrix}U_{11} V_{11}+U_{12} V_{21} & U_{11} V_{12}+U_{12} V_{22} \\\\\\\\ 
    U_{21} V_{11}+U_{22} V_{21} & U_{21} V_{12}+U_{22} V_{22}\end{pmatrix}}\parentheses{x_i^a x_j^b}\\\\\\\\
    &= f(U \circ V) \parentheses{x_i^a x_j^b},
\end{align}

showing that $f(U)\circ f(V) = f(U \circ V)$ and thus $f$ is a homomorphism. {% include endproof.html %}

The only remaining step is to show that $f(U)$ is indeed unitary, which will validate the choice of the $\sqrt{n_i!}$ terms in \eqref{eq:monomial-def} since they are necessary for the proof.


**Theorem:** Let $f$ be as defined in \eqref{eq:f}. If $U \in U(m)$, then $f(U) \in U(M)$.

*Proof:* Without loss of generality, we can restrict our attention to unitaries $U$ that act on only two modes $i$ and $j$, and to the action of $f(U)$ on computational basis states $\frac{x_i^{a}x_j^b}{\sqrt{a! b!}}$. By the previous theorem, $f(U^\dagger)$ is the inverse of $f(U)$. All that is left to show, then, is that $f(U^\dagger) = f(U)^\dagger$. To be totally clear, I will notate $\ket{a,b} = \frac{x_i^a x_j^b}{\sqrt{a!b!}}$.

\begin{align}
    f(U)\ket{a,b} &= \frac{1}{\sqrt{a!b!}}\parentheses{U_{11} x_i + U_{21}x_j}^a \parentheses{U_{12}x_i + U_{22}x_j}^b\\\\\\\\
    &= \frac{1}{\sqrt{a!b!}}\sum_{s=0}^a\sum_{t=0}^b \binom{a}{s}\binom{b}{t}U_{11}^sU_{21}^{a-s}U_{12}^tU_{22}^{b-t}x_i^{s+t}x_j^{a+b-s-t}\\\\\\\\
    &= \sum_{s=0}^a\sum_{t=0}^b \binom{a}{s}\binom{b}{t}\sqrt{\frac{(s+t)!(a+b-s-t)!}{a!b!}}\\\\\\\\
    &~ \times U_{11}^sU_{21}^{a-s}U_{12}^tU_{22}^{b-t}\ket{s+t,a+b-s-t}.
\end{align}

Therefore, the matrix elements of $f(U)$ are

\begin{align}
    \bra{c,d}f(U)\ket{a,b} &= \sum_{s=0}^a\sum_{t=0}^b \binom{a}{s}\binom{b}{t}\sqrt{\frac{c!d!}{a!b!}}U_{11}^sU_{21}^{a-s}U_{12}^tU_{22}^{b-t} \delta_{s+t,c}\delta_{a+b-c,d}\\\\\\\\
    &= \sum_{s=0}^a \binom{a}{s}\binom{b}{c-s}\sqrt{\frac{c!d!}{a!b!}}U_{11}^sU_{21}^{a-s}U_{12}^{c-s}U_{22}^{b-c+s} \delta_{a+b,c+d},
\end{align}

from which the matrix elements of $f(U^\dagger)$ and $f(U)^\dagger$ can be computed as

\begin{align}
    \bra{c,d}f(U^\dagger)\ket{a,b} &= \sum_{s=0}^a \binom{a}{s}\binom{b}{c-s}\sqrt{\frac{c!d!}{a!b!}}\bar U_{11}^s \bar U_{12}^{a-s} \bar U_{21}^{c-s} \bar U_{22}^{b-c+s} \delta_{a+b,c+d}\\\\\\\\
    \bra{c,d}f(U)^\dagger \ket{a,b} &= \sum_{s=0}^c \binom{c}{s}\binom{d}{a-s}\sqrt{\frac{a!b!}{c!d!}}\bar U_{11}^s \bar U_{21}^{c-s}\bar U_{12}^{a-s}\bar U_{22}^{b-c+s} \delta_{a+b,c+d}.
\end{align}

These two expressions are equal provided that

\begin{equation}
    \binom{a}{s}\binom{b}{c-s}\sqrt{\frac{c!d!}{a!b!}} = \binom{c}{s}\binom{d}{a-s}\sqrt{\frac{a!b!}{c!d!}}
\end{equation}

whenever $a+b=c+d$, which is straightforward to verify. Thus, we have proven that $f(U^\dagger) = f(U)^\dagger$, and indeed the $\sqrt{n_i!}$ terms in \eqref{eq:monomial-def} were essential. {% include endproof.html %}


### Relationship to the permanent

Note that $[m]^{[n]}$ denotes the set of maps with domain $[n]$ and codomain $[m]$.

**Definition** *(Multiplicity function):* Let $f^{-1}[b] \subseteq A$ denote the preimage of $b \subseteq B$ under the map $f\colon A \to B$. For a map $\sigma\colon [n]\to [m]$, define its multiplicity function $\calM_\sigma\colon [m] \to \curlybrackets{0} \cup [n]$ by $j \mapsto \abs{\sigma^{-1}[\curlybrackets{j}]}$. In words, the multiplicity function indicates how many elements in the domain of $\sigma$ map to a particular value in the codomain of $\sigma$. Finally, for each map $\sigma \in [m]^{[n]}$, define its equivalence class $[\sigma] \coloneqq \curlybrackets{\sigma' \in [m]^{[n]}\mid \calM_\sigma = \calM_{\sigma'}}$. Two maps $\sigma, \sigma'$ are said to be *equivalent* if they belong to the same equivalence class, and *inequivalent* otherwise. {% include endproof.html %}

**Example:** Suppose $n = 3$, $m = 3$, and $\sigma\colon [n]\to[m]$ such that $\sigma(1) = \sigma(2) = 1$ and $\sigma(3) = 2$. The multiplicity function is $\calM_\sigma(1) = 2$, $\calM_\sigma(2) = 1$, and $\calM_\sigma(3) = 0$. The equivalence class is $[\sigma] = \curlybrackets{\sigma, \sigma', \sigma^{\prime\prime}}$, where $\sigma'(1) = 2$, $\sigma'(2) = \sigma'(3) = 1$, $\sigma^{\prime\prime}(2) = 1$, and $\sigma^{\prime\prime}(1) = \sigma^{\prime\prime}(3) = 1$. {% include endproof.html %}

Suppose we begin in the state

\begin{equation}
    \label{eq:psi0}
    \ket{\psi\_0} \coloneqq \lvert \underbrace{1\dots 1}\_{n} ~ \underbrace{0\dots 0}\_{m-n} \rangle
\end{equation}

and apply a unitary $U$ on the $m$ modes. Then

\begin{equation}
    f(U)\ket{\psi_0} \longleftrightarrow f(U)\parentheses{\prod_{i=1}^n x_i} = \prod_{i=1}^{n} \sum_{j=1}^m U_{ji}x_j.
\end{equation}

Fix some map $\sigma\colon [n] \to [m]$; then the coefficient in front of the $\prod_{i=1}^n x_{\sigma(i)} = \prod_{i=1}^m x_i^{\calM_\sigma(i)}$ term is $\prod_{i=1}^n U_{\sigma(i)i}$. Notice, though, that this respects the ordering of the formal variables $x_i$. Since the formal variables commute, we are interested in the coefficients of the (unnormalized) terms $\prod_{i=1}^n x_{\sigma'(i)}$ for each $\sigma' \in [\sigma]$. The point is simply that $\prod_{i=1}^n x_{\sigma(i)} = \prod_{i=1}^n x_{\sigma'(i)} = \prod_{i=1}^m x_i^{\calM_\sigma(i)}$ for every $\sigma' \in [\sigma]$ since the formal variables commute.

Therefore, the coefficient of interest is

\begin{equation}
    \alpha_{[\sigma]} = \sum_{\sigma' \in [\sigma]}\prod_{i=1}^n U_{\sigma'(i)i}.\label{eq:alpha_sigma}
\end{equation}

The probability of measuring the output state $\ket{\bm n}$ from $f(U)\ket{\psi_0}$ is $\Pr[\bm n] = \abs{\bra{\bm n}f(U) \ket{\psi_0}}^2$. An equivalence class $[\sigma]$ corresponds to an $\bm n$ by its multiplicity function; in particular, $n_i = \calM_\sigma(i)$ for each mode $i \in [m]$. Therefore the probability of measuring the output state associated to $[\sigma]$ is 

\begin{equation}
    \label{eq:probability}
    \Pr[\bm n] = \abs{\alpha_{[\sigma]}}^2 \prod_{i=1}^m n_i!,
\end{equation}

where the factorials have been reintroduced to account for the normalization of the monomial.


**Example** *(Probability distribution over $H_{2,2}$):* Beginning with $\ket{\psi_0} = \ket{11}$, \eqref{eq:probability} can be used to determine $\Pr[(2,0)]$, $\Pr[(1,1)]$, and $\Pr[(0,2)]$.

- For $\Pr[(2,0)]$, the $\sigma \in [m]^{[n]}$ describing $(2,0)$ is $\sigma(1) = \sigma(2) = 1$ so that the monomial term is $x_{\sigma(1)}x_{\sigma(2)} = x_1^2$. The multiplicity function is $\calM_\sigma(1) = 2$, $\calM_\sigma(2) = 0$ so that $\bm n = (2, 0)$. There is only one such $\sigma$ describing the monomial, thus $[\sigma] = \curlybrackets{\sigma}$. Therefore, $\Pr[(2,0)] = 2\abs{U_{11}U_{12}}^2$.
- For $\Pr[(1,1)]$, one possible $\sigma$ describing $(1,1)$ is $\sigma(1) = 1$ and $\sigma(2) = 2$ so that the monomial term is $x_{\sigma(1)}x_{\sigma(2)} = x_1x_2$. Another one is $\sigma'$ with $\sigma'(1) = 2$ and $\sigma'(2) = 1$. Clearly, $\sigma$ and $\sigma'$ are in the same equivalence class since their multiplicity functions both satisfy $\calM(1) = \calM(2) = 1$ resulting in $\bm n = (1,1)$, and thus they result in the same monomial. As such, $[\sigma] = \curlybrackets{\sigma,\sigma'}$. Therefore, $\Pr[(1,1)] = \abs{U_{11}U_{22} + U_{21}U_{12}}^2$.
- For $\Pr[(0,2)]$, the $\sigma$ describing $(0,2)$ is $\sigma(1) = \sigma(2) = 2$ so that the monomial term is $x_{\sigma(1)}x_{\sigma(2)} = x_2^2$. In this case, the multiplicity function is $\calM_\sigma(1) = 0$, $\calM_\sigma(2) = 2$ so that $\bm n = (0,2)$. Clearly, $[\sigma] = \curlybrackets{\sigma}$. Therefore, $\Pr[(0,2)] = 2\abs{U_{21}U_{22}}^2$.

This reproduces the result from \eqref{eq:f-example}. {% include endproof.html %}

This example hints at a relationship between $\Pr[\bm n]$ and the permanent of $U$. Indeed, $\Pr[(1,1)] = \abs{\perm(U)}^2$ by the definition of the permanent

\begin{equation}
    \label{eq:permanent}
    \perm(A) \coloneqq \sum_{\pi \in S_N} \prod_{i=1}^N A_{\pi(i),i}
\end{equation}

for an $N\times N$ matrix. Additionally,

\begin{equation}
    \Pr[(2,0)] = \frac{1}{2}\abs{\perm\pargs{\begin{matrix}U_{11}&U_{12}\\\\\\\\
    U_{11}&U_{12}\end{matrix}}}^2,\label{eq:repeated-rows-ex}
\end{equation}

and the expression for $\Pr[(0,2)]$ is similar. By examination of \eqref{eq:alpha_sigma}, the result can be extrapolated as follows. For a general $m\times m$ unitary matrix $U$ representing a linear-optic network on $m$ modes, define $U_{\bm n}$ to be the $n \times n$ matrix formed from $U$ by first removing columns $n+1$ through $m$, and then repeating each row $r$ a total of $n_r$ times. Then,

\begin{equation}
    \label{eq:BSEquation}
    \Pr[\bm n] = \frac{\abs{\perm(U_{\bm n})}^2}{\prod_{i=1}^m n_i!}.
\end{equation}

The connection between bosons and the permanent is the basis for the computation complexity of BosonSampling.


## Linear optics formulation

Suppose $V(t) = e^{i H t}$ where $H = \sum_{ij} h_{ij}a_i^\dag a_j$. We will assume that $h_{ij} = \bar h_{ji}$ so that $H$ is Hermitian and $V$ is unitary. The $a_k$ operators obey the standard bosonic commutation relations. A state with occupation numbers $\ket{\bm n} = \ket{n_1\dots n_m}$ is $\prod_{i=1}^m\frac{a_i^{\dag n_i}}{\sqrt{n_i!}}\ket{0^m}$. The factorial is necessary for normalization and is indeed the reason for the factorials in \eqref{eq:monomial-def}.

A simple exercise verifies that

\begin{equation}
    \comm{H}{a_k} = -\sum_j h_{kj}a_j.
\end{equation}

Define $a_k(t) = V(t) a_k V^\dagger(t)$. Then,

\begin{align}
    \partial_t a_k(t) &= i V(t) \comm{H}{a_k} V^\dagger(t)\\\\\\\\
    &= -i \sum_j h_{kj} V(t) a_j V^\dagger(t)\\\\\\\\
    &= -i \sum_j h_{kj}a_j(t).
\end{align}

This is simply a linear equation, and can expressed in matrix notation. Associate a vector $\ket{k(t)} \leftrightarrow a_k(t)$. Then the corresponding equation is $\partial_t \ket{k(t)} = -i h^T\ket{k(t)}$, which is solved by $\ket{k(t)} = e^{-i h^T t}\ket{k(0)}$. Therefore, $a\_k(t) = \sum\_j (e^{-i h^T t})\_{kj}a\_j(0)$, or equivalently

\begin{equation}
a\_k^\dagger(t) = \sum\_{j} (e^{ih^T t})\_{kj}a\_j^\dagger(0).
\end{equation}

This finally brings us the important result that

\begin{equation}
    V(1) a_k^\dagger V^\dagger(1) = \sum_{j}U_{jk}a_j^\dagger
\end{equation}

where $U \coloneqq e^{i h}$. 

A passive linear-optics network can implement a unitary $V = e^{i H}$ on a set of $m$ modes, for a Hamiltonian $H = \sum_{i,j=1}^m h_{ij}a_i^\dag a_j$ ([source][linoptics]). A passive linear-optics unitary will not affect photon number. Evolving $\ket{\psi_0}$ from \eqref{eq:psi0} with $V$ results in

\begin{align}
    V \ket{\psi_0} &=  V \parentheses{\prod_{j=1}^n a_j^\dag} \ket{0^m}\\\\\\\\
    &= \parentheses{\prod_{j=1}^n Va_j^\dag V^\dag} V\ket{0^m}\\\\\\\\
    &= \prod_{j=1}^n \sum_{i}U_{ij}a_i^\dagger\ket{0^m}\\\\\\\\
    &= \sum_{[\sigma]}\alpha_{[\sigma]} \prod_{j=1}^m a_{\sigma(j)}^\dag\ket{0^m}
\end{align}

where we used the fact that $V \ket{0^m} = \ket{0^m}$. Recall that a $[\sigma]$ defines a $\bm n$ by its multiplicity function. In this case,

\begin{align}
    \Pr[\bm n] &= \abs{\alpha_{[\sigma]} \bra{\bm n}\prod_{j=1}^m a_{\sigma(j)}^\dag\ket{0^m}}^2\\\\\\\\
    &= \abs{\alpha_{[\sigma]} \bra{\bm n}\prod_{j=1}^m \sqrt{n_i!}~\frac{a_{\sigma(j)}^\dag}{\sqrt{n_i!}}\ket{0^m}}^2\\\\\\\\
    &= \abs{\alpha_{[\sigma]} \prod_{j=1}^m \sqrt{n_i!} \bra{\bm n}\ket{\bm n}}^2\\\\\\\\
    &= \abs{\alpha_{[\sigma]}}^2\prod_{i=1}^m n_i!,
\end{align}

which reproduces \eqref{eq:probability}!

From this, one can imagine the scenario in which the $a_i$ operators are fermionic instead of bosonic. In this case, the anticommutation relations give rise to various sign factors that ultimately results in the determinant showing up as opposed to the permanent. Interestingly, the determinant can be computed in polynomial time using LU decomposition along with the property that $\det(LU) = \det(L)\det(U)$, indicating that FermionSampling may be computationally easy (indeed it turns out that it is).

Understanding BosonSampling from the linear optics point of view helps us to understand other potential variants of the experiment. For example, one alternative to the input state $\ket{\psi_0} = \ket{1^n 0^{m-n}}$ is instead a product state of *coherent states*. A coherent state defined by $\alpha \in \bbC$ on one mode is $\ket{\phi(\alpha)} = e^{-\abs{\alpha}^2/2}e^{\alpha a^\dagger} \ket{0}$. The outputs of standard lasers can be thought of as coherent states. Therefore, if we replace the single photon source in BosonSampling by laser light, the resulting input state is

\begin{equation}
    \ket{\psi\_0^c(\alpha)} = \lvert \underbrace{\phi(\alpha)\dots\phi(\alpha)}\_{n} ~ \underbrace{0\dots0}\_{m-n}\rangle = e^{-n\abs{\alpha}^2 / 2}\parentheses{\prod\_{i=1}^n e^{\alpha a\_i^\dagger}}\ket{0^m}.
\end{equation}

After sending $\ket{\psi_0^c}$ through a linear optic network $V$, the output state is

\begin{align}
    V\ket{\psi_0^c(\alpha)} &= e^{-n\abs{\alpha}^2 / 2}\parentheses{\prod_{i=1}^n e^{\alpha V a_i^\dagger V^\dagger}}V\ket{0^m}\\\\\\\\
    &= e^{-n\abs{\alpha}^2 / 2}\parentheses{\prod_{i=1}^n \exp(\alpha \sum_{j=1}^m U_{ji}a_j^\dagger)}\ket{0^m}\\\\\\\\
    &= e^{-n\abs{\alpha}^2 / 2}\parentheses{\prod_{j=1}^m \exp(\alpha \sum_{i=1}^n U_{ji}a_j^\dagger)}\ket{0^m}\\\\\\\\
    &= \ket{\phi\pargs{\alpha\sum_{i=1}^n U_{1i}}~\dots~\phi\pargs{\alpha\sum_{i=1}^n U_{mi}}}.\label{eq:coherentbs}
\end{align}

Crucially, we have used that all of the $a_i^\dagger$ commute so the exponentials of operators can be treated as if they are simply exponentials of numbers.

The output state is completely determined by \eqref{eq:coherentbs}, and is simply a product state of single mode coherent states. In particular, the properties of the output coherent state on mode $j$ can be completely determined in $\bigO{n}$ time by calculating $\alpha_j' \coloneqq \alpha\sum_{i=1}^n U_{ji}$. For example, the expected photon number in the $j^{\rm th}$ mode prior to $V$ is $\abs{\alpha}^2$ when $j \leq n$ and 0 otherwise. After $V$, the expected photon number in the $j^{\rm th}$ mode is $\lvert\alpha_j'\rvert^2$, which is efficiently computable classically. Using properties of unitary matrices, one can show that $\sum_{j=1}^m \lvert\alpha_j'\rvert^2 = n\abs{\alpha}^2$, which is consistent with the fact that $V$ preserves photon number.

We have shown that BosonSampling with coherent/laser input states (without access to non-demolition photon number measurements; with access to non-demolition photon measurements, one could prepare $\ket{\psi_0^c(1)}$ and simply postselect on one photon being in each mode) is a classically computationally easy task, whereas single photon input states is not. Once can ask a similar question about *squeezed* input states. In this case, the input on each mode is $\exp(re^{-i\theta} a^2 -re^{i\theta} a^{\dagger 2})\ket 0$. The same analysis as with coherent states does not hold here because of the complicated non-commuting terms in the exponential. Indeed, squeezed state inputs are not thought to be easily simulable, and are in fact the basis for [*Gaussian* BosonSampling][Hamilton2017].



[BS2013]: https://www.theoryofcomputing.org/articles/v009a004/v009a004.pdf
[linoptics]: https://link.aps.org/doi/10.1103/PhysRevA.65.032325
[Hamilton2017]: https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.119.170501
[DecompOfLinearOpticUnitary]: https://link.aps.org/doi/10.1103/PhysRevLett.73.58


{% include post-footer.html %}
