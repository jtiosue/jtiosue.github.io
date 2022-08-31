---
title: Why is classical mechanics symplectic?
comments: 32
---

{% include post-header.md %}

(30 Aug 2022) First, we consider a smooth manifold $N$ representing configuration space. Ultimately, we want to consider dynamics from an initial position and initial velocity. Hence, we also want our manifold to have velocity information. One can therefore either go to the tangent bundle $TN$ or the cotangent bundle $T^\ast N$. Roughly speaking, Lagrangian mechanics takes place on the tangent bundle (coordinates and velocities) while Hamiltonian mechanics takes place on the cotangent bundle (momentum are dual to velocities in the sense that they are linear maps from tangent vectors to real numbers). Therefore, we consider the *phase space* $M = T^\ast N$. 

Next, we consider that there is some function $H\colon M \to \reals$ that determines dynamics. $H$ will of course represent the Hamiltonian. An initial condition is just a point on $M$. Hence, the dynamics induced by $H$ can be described without reference to any particular initial condition by considering a vector field. Specifically, for every Hamiltonian $H$ on $M$, there is an associated *Hamiltonian vector field* $X_H \in \mathcal X(M) = \Gamma(M,TM)$. We are therefore tasked with determining $X_H$ from $H$.

Consider now a point $p\in M$. The dynamics at $p$ should depend only on how $H(p)$ differs from $H(p^\prime)$ for nearby points $p^\prime$. Hence, if $V \in T_p M$ is a vector at $p$, then the dynamics should only depend on $V(H)$, the derivative of $H$ in the direction of $V$. Recall that $V(H) = dH\rvert_p(V)$, where $dH\rvert_p \in T^\ast _pM$ is the exact one form defined by $H$. This should be true for any $V$, and hence $X_H\rvert_p$ should depend only on $dH\rvert_p$, not $H$ itself. We are therefore led to

$$
\text{something involving } X_H = \text{something involving }dH.
$$

The obvious problem is that $X_H$ is a vector field and $dH$ is a one form. So we need to make them compatible. We will convert the left-hand side to a one form. One way to do this is to consider a map $\omega \colon TM \times TM \to \reals$. Let $i_V$ be the interior product $(i_V \omega)(W) = \omega(V, W)$. Then $i_{X_H}\omega$ is a one form if we require $\omega$ to be linear in the second argument. So we are led to the equation

$$
i_{X_H}\omega = dH.
$$

Recall that we are just trying to figure out the relationship between $X_H$ and $H$, which we can now do by figuring out what $\omega$ is.

The next thing to argue is that $\omega$ is also linear in the first argument. I’m not totally sure of a good argument here, but there a couple of things to say. The most obvious answer is that we are working on a manifold with tensor fields, so the most natural guess would be for $\omega$ to be multilinear. I think there may also be another argument about how making $\omega$ multilinear results in linear differential equations for the dynamics, which is perhaps desirable. Anyways, I’m not totally sure how to motivate this step, but it definitely does seem like the most natural choice.

We have therefore found that at each point $p\in M$, $\omega_p$ is a multilinear maps from $T_p M\times T_p M \to \reals$, or in other words an element of $T^\ast _p M \otimes T^\ast _p M$. I.e., $\omega$ is a section of $T^\ast M\otimes T^\ast M$. We want that energy is conserved throughout the dynamics. Therefore, the derivative of $H$ along the vector field $X_H$ should be zero. This amounts to $X_H(H) = 0$, or equivalently $dH(X_H) = 0$. Thus, $(i_{X_H}\omega)(X_H) = \omega(X_H,X_H) = 0$. This should be true for any Hamiltonian, and hence $\omega$ must be alternating. We can see this as follows:

$$
\begin{aligned}
\omega(X,Y) &= \omega(X,Y) + \omega(X,X) \qquad \text{since }\omega(X,X)=0\\
&= \omega(X,X+Y) \qquad \text{since }\omega\text{ is multilinear}\\
&= \omega(X+Y-Y, X+Y)\\
&= \omega(X+Y,X+Y)-\omega(Y,X+Y)\\
&= -\omega(Y,X+Y)\\
&= -\omega(Y,X).
\end{aligned}
$$

We have therefore determined that $\omega$ is a two-form $\omega \in \Omega^2(M)$, since it is a bilinear alternating form.

We also want that every Hamiltonian results in a Hamiltonian vector field. I.e. every system has a dynamical solution; we should always be able to solve for $X_H$. Therefore, $\omega$ should be nondegenerate.

In summary, we have determined that the dynamics $X_H$ are derived from the Hamiltonian $H$ via a nondegenerate two-form $\omega$ on phase space $M$. The only remaining ingredient to show that $(M,\omega)$ is a symplectic manifold — i.e. that $\omega$ is a symplectic form — is to show that $\omega$ is closed. We do that now. 

Suppose that $f_t\colon M \to M$ represents time evolution by a time $t$. In other words, each point in the manifold representing position and momentum get mapped via $f_t$ to a new position and momentum. We want the dynamics to be independent of time translation. $\omega$ is what is determining how the dynamics arise from $H$, and hence we want that the pullback $f_t^\ast \omega = \omega$. Therefore,

$$
\frac{d}{dt} f_t^\ast \omega = 0.
$$

Since time evolution by definition generates a flow along $X_H$, we see that $\frac{d}{dt}f_t^\ast \omega$ is precisely the definition of the Lie derivative $L_{X_H}\omega$. Therefore,

$$
L_{X_H}(\omega) = 0.
$$

We use the formula

$$
L_{X_H}\omega = i_{X_H}(d\omega) + d(i_{X_H}\omega)= i_{X_H}(d\omega) + d^2H = i_{X_H}(d\omega).
$$

This should be zero for all $H$, so we find that $\omega$ must be closed, $d\omega = 0$.

We have therefore found that $\omega$ is a symplectic form and therefore that phase space $(M,\omega)$ is a symplectic manifold.


#### References

- [https://math.mit.edu/~cohn/Thoughts/symplectic.html](https://math.mit.edu/~cohn/Thoughts/symplectic.html)


{% include post-footer.html %}
