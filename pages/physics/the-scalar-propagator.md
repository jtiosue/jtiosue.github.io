---
title: The scalar propagator
comments: 21
---

{% include post-header.md %}

(21 May 2021) In this post, we will derive the Feynman propagator for a real scalar field. Much of the discussion of course generalizes to complex scalar fields, and to other types of fields. Please note that I will use the metric convension $(+---)$ throughout this post.

The propagator is a Green's function, and there are various choices such as the retarded, advanced, and Feynman propagators. For a more complete discussion on these topics, see e.g. [here](https://www.desy.de/~jlouis/Vorlesungen/QFTI10/QFTI.pdf) and [here](https://en.wikipedia.org/wiki/Propagator#Scalar_propagator). People have different definitions of propagators, and different interpretations of what they do. Ultimately, though, I think the simplest way to understand them is by defining the Feynman propagator as

$$D(x-y) = \bra 0 T\cbargs{\phi(x) \phi(y)} \ket 0$$

and noting that due to Wick's theorem such an object shows up everywhere in perturbation theory. Hopefully I'm not missing something major, but I don't really think there is too much more to it than that.


## The classical field

We begin with the Klein-Gordan Lagrangian density

$$\calL(x) = \frac{1}{2}\partial_\mu \phi(x) \partial^\mu \phi(x) - \frac{1}{2}m^2 \phi(x)^2,$$

where $x$ is a four-vector. The equations of motion are

$$\frac{\delta \calL}{\delta \phi} = \partial_\mu \frac{\delta \calL}{\delta \partial_\mu \phi},$$

giving

$$\parentheses{\partial_\mu \partial^\mu + m^2} \phi(x) = 0.$$

We then Fourier transform the position part of $x$ so that

$$\phi(t, \bm x) = \int \frac{d^3 p}{(2\pi)^3}e^{i \bm p \cdot \bm x} \widetilde \phi(t, \bm p).$$

Then

$$\begin{aligned}
    0 &= \parentheses{\partial_\mu \partial^\mu + m^2} \phi(x) \\
    &= \int \frac{d^3 p}{(2\pi)^3} \parentheses{\partial_\mu \partial^\mu + m^2} e^{i \bm p\cdot \bm x}\widetilde\phi(t, \bm p) \\
    &= \int \frac{d^3 p}{(2\pi)^3} \parentheses{\partial_t^2 + \bm p \cdot \bm p + m^2} e^{i \bm p\cdot \bm x}\widetilde \phi(t, \bm p).
\end{aligned}$$

So, for each momentum, $\parentheses{\partial_t^2 + \bm p^2+ m^2}\widetilde \phi(t, \bm p)$. This is the equation for a harmonic oscillator with frequency $\omega_{\bm p}^2 = \bm p^2 + m^2$. Thus the solution is

$$\widetilde \phi(t, \bm p) = \frac{1}{\sqrt{2 \omega_{\bm p}}}\parentheses{a_{\bm p}^{(1)} e^{-i \omega_{\bm p} t} + a_{\bm p}^{(2)} e^{i \omega_{\bm p} t}}$$

for some constants $a_{\bm p}^{(1)}$ and $a_{\bm p}^{(2)}$. Note that the $\sqrt{2 \omega_{\bm p}}$ normalization factor is arbitrary and thus a convention, but by choosing such a normalization the $a_{\bm p}$'s will turn out to be the standard harmonic oscillator ladder operators. In summary, we have found that the Klein-Gordan equation is equivalent to a harmonic oscialltor for every momentum. Going back to real space, then, we find

$$\begin{aligned}
\phi(t, \bm x) &= \int \frac{d^3 p}{(2\pi)^3}e^{i \bm p \cdot \bm x} \frac{1}{\sqrt{2 \omega_{\bm p}}}\parentheses{a_{\bm p}^{(1)} e^{-i \omega_{\bm p} t} + a_{\bm p}^{(2)} e^{i \omega_{\bm p} t}}\\
&= \int \frac{d^3 p}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}}}\parentheses{a_{\bm p}^{(1)} e^{-i p_\mu x^\mu} + a_{\bm p}^{(2)} e^{i p_\mu x^\mu}},
\end{aligned}$$

where $p_0 = \omega_{\bm p}$. Since we are summing that $\phi$ is real (i.e. real scalar field theory), we require that $\phi(t, \bm x)^\ast = \phi(t, \bm x)$, meaning that $a_{\bm p}^{(1)} = a_{\bm p}^{(2)\ast}$. Let's rename $a_{\bm p}^{(1)}$ to simply $a_{\bm p}$. Then $a_{\bm p}^{(2)} = a_{\bm p}^\ast$, giving

\begin{equation}
\label{eq:classicalphi}
\phi(t, \bm x) = \int \frac{d^3 p}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}}}\parentheses{a_{\bm p} e^{-i p_\mu x^\mu} + a_{\bm p}^\ast e^{i p_\mu x^\mu}}.
\end{equation}

Note that in complex scalar field theory, one does not require that $\phi(t, \bm x)^\ast = \phi(t, \bm x)$. All the steps we take here are very similar with complex scalar field theory with minor modifications.


## Quantizing the scalar field

To quantize the field \eqref{eq:phi}, one promotes the $a_{\bm p}$ to operators (also meaning that $a_{\bm p}^\ast \to a_{\bm p}^\dagger$) and enforces the canonical commutation relations

$$\comm{\phi(t, \bm x)}{\pi(t, \bm y)} = i\delta^3(\bm x - \bm y)$$

between $\phi$ and its conjugate momentum density

$$\begin{aligned}
\pi(t, \bm y) &= \frac{\delta \calL}{\delta \partial_t \phi}\\
&= \partial_t \phi(t, \bm y)\\
&= i \int \frac{d^3 p}{(2\pi)^3} \sqrt{\frac{\omega_{\bm p}}{2}}\parentheses{-a_{\bm p} e^{-i p_\mu y^\mu} + a_{\bm p}^\dagger e^{i p_\mu y^\mu}}.
\end{aligned}$$

By defining $\widetilde \pi(t, \bm p)$ as we did $\widetilde \phi(t, \bm p)$, we find that

$$\widetilde\pi(t, \bm p) = \partial_t \widetilde\phi(t, \bm p) = sqrt{\frac{\omega_{\bm p}}{2}}\parentheses{-a_{\bm p} e^{-i \omega_{\bm p} t} + a_{\bm p}^\dagger e^{i \omega_{\bm p} t}}.$$

As such, the commutation relations become

$$\comm{\widetilde \phi(t, \bm p)}{\widetilde \pi(t, \bm q)} = i (2\pi)^3 \delta^3(\bm p - \bm q).$$

Using

$$a_{\bm p}e^{-i \omega_{\bm p} t} = \frac{1}{2}\parentheses{\sqrt{2\omega_{\bm p}} \widetilde \phi(t, \bm p) + i \sqrt{\frac{2}{\omega_{\bm p}}} \widetilde \pi(t, \bm p)},$$

we find

$$\begin{aligned}
  \comm{a_{\bm p}}{a_{\bm q}}e^{-i t (\omega_{\bm p}+\omega_{\bm q})} &= \frac{i}{2}\parentheses{\sqrt{\frac{\omega_{\bm p}}{\omega_{\bm q}}} \comm{\widetilde\phi(t, \bm p)}{\widetilde \pi(t, \bm q)} + \sqrt{\frac{\omega_{\bm q}}{\omega_{\bm p}}} \comm{\widetilde\pi(t, \bm p)}{\widetilde \phi(t, \bm q)} }\\
  &= -\frac{(2\pi)^3}{2}\parentheses{\sqrt{\frac{\omega_{\bm p}}{\omega_{\bm q}}} \delta^3(\bm p - \bm q) - \sqrt{\frac{\omega_{\bm q}}{\omega_{\bm p}}} \delta^{3}(\bm q - \bm p) }\\
  &= 0,
\end{aligned}$$

and

$$\begin{aligned}
  \comm{a_{\bm p}}{a_{\bm q}^\dagger}e^{-i t (\omega_{\bm p}-\omega_{\bm q})} &= \frac{i}{2}\parentheses{-\sqrt{\frac{\omega_{\bm p}}{\omega_{\bm q}}} \comm{\widetilde\phi(t, \bm p)}{\widetilde \pi(t, \bm q)} + \sqrt{\frac{\omega_{\bm q}}{\omega_{\bm p}}} \comm{\widetilde\pi(t, \bm p)}{\widetilde \phi(t, \bm q)} }\\
  &= -\frac{(2\pi)^3}{2}\parentheses{-\sqrt{\frac{\omega_{\bm p}}{\omega_{\bm q}}} \delta^3(\bm p - \bm q) - \sqrt{\frac{\omega_{\bm q}}{\omega_{\bm p}}} \delta^{3}(\bm q - \bm p) }\\
  &= (2\pi)^3} \delta^3(\bm p - \bm q).
\end{aligned}$$

So we see that $a_{\bm p}$ is an annihilation operator, and the corresponding creation operator is $a_{\bm p}^\dagger.$ In the end, the quantized scalar field $\phi$ is

\begin{equation}
  \label{eq:quantumphi}
  \phi(x) = \int \frac{d^3 p}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}}}\parentheses{a_{\bm p} e^{-i p_\mu x^\mu} + a_{\bm p}^\dagger e^{i p_\mu x^\mu}},
\end{equation}

where $a_{\bm p}$ obey bosonic creation/annihilation operator commutation relations.


## The scalar propagator

From \eqref{eq:quantumphi}, we can now derive the scalar propagator. Let $D(x-y)$ be the Feynman propagator ($x$ and $y$ are four-vectors) defined as

$$\begin{aligned}
D(x-y) &= \bra 0 T \cbargs{\phi(x) \phi(y)} \ket 0\\
&= \Theta\pargs{x^0 - y^0}\bra 0 \phi(x) \phi(y) \ket 0 + \Theta\pargs{y^0 - x^0}\bra 0 \phi(y) \phi(x) \ket 0,
\end{aligned}$$

where $\Theta$ is the Heaviside step function. We have that

$$\begin{aligned}
\bra 0 \phi(x) \phi(y) \ket 0 &= \bra 0 \int \frac{d^3 p}{(2\pi)^3}\frac{d^3 q}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}2 \omega_{\bm q}}}\parentheses{a_{\bm p} e^{-i p_\mu x^\mu} + a_{\bm p}^\dagger e^{i p_\mu x^\mu}}\parentheses{a_{\bm q} e^{-i q_\mu y^\mu} + a_{\bm q}^\dagger e^{i q_\mu y^\mu}} \ket 0\\
&= \bra 0 \int \frac{d^3 p}{(2\pi)^3}\frac{d^3 q}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}2 \omega_{\bm q}}}\parentheses{a_{\bm p} e^{-i p_\mu x^\mu}}\parentheses{a_{\bm q}^\dagger e^{i q_\mu y^\mu}} \ket 0\\
&= \bra 0 \int \frac{d^3 p}{(2\pi)^3}\frac{d^3 q}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}2 \omega_{\bm q}}} e^{i q_\mu y^\mu-i p_\mu x^\mu}  \bra 0 a_{\bm p} a_{\bm q}^\dagger \ket 0\\
&= \bra 0 \int \frac{d^3 p}{(2\pi)^3}\frac{d^3 q}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}2 \omega_{\bm q}}} e^{i q_\mu y^\mu-i p_\mu x^\mu}  \bra 0 (2\pi)^3 \delta^3(\bm p - \bm q) +  a_{\bm q}^\dagger a_{\bm p}  \ket 0\\
&=  \int \frac{d^3 p}{(2\pi)^3}\frac{d^3 q}{(2\pi)^3} \frac{1}{\sqrt{2 \omega_{\bm p}2 \omega_{\bm q}}} e^{i q_\mu y^\mu-i p_\mu x^\mu} (2\pi)^3 \delta^3(\bm p - \bm q)\\
&= \int \frac{d^3 p}{(2\pi)^3} \frac{1}{2 \omega_{\bm p}} e^{i p_\mu (y^\mu- x^\mu)}.
\end{aligned}$$

Therefore,

$$\begin{aligned}
  D(x-y) &= \Theta\pargs{x^0 - y^0}\bra 0 \phi(x) \phi(y) \ket 0 + \Theta\pargs{y^0 - x^0}\bra 0 \phi(y) \phi(x) \ket 0\\
  &= \int \frac{d^3 p}{(2\pi)^3} \frac{1}{2 \omega_{\bm p}} \parentheses{ \Theta\pargs{x^0 - y^0}e^{i p_\mu (y^\mu- x^\mu)} + \Theta\pargs{y^0 - x^0}e^{i p_\mu (x^\mu- y^\mu)} }\\ 
  &= \int \frac{d^3 p}{(2\pi)^3} \frac{1}{2 \omega_{\bm p}} \parentheses{ \Theta\pargs{x^0 - y^0}e^{i p_\mu (y^\mu- x^\mu)} + \Theta\pargs{y^0 - x^0}e^{-i p_\mu (y^\mu- x^\mu)} }\\.
  &= \int \frac{d^3 p}{(2\pi)^3} \frac{1}{2 \omega_{\bm p}} \parentheses{ \Theta\pargs{x^0 - y^0}e^{-i p_\mu (x^\mu- y^\mu)} + \Theta\pargs{y^0 - x^0}e^{i p_\mu (x^\mu- y^\mu)} }.
\end{aligned}$$

One can then verify using the residue theorem that

$$D(x-y) = \int \frac{d^4 p}{(2\pi)^4} \frac{i}{p_\mu p^\mu - m^2 + i \epsilon} e^{-i p_\mu (x^\mu - y^\mu)},$$

with $\epsilon \to 0$. Notice that $\sgn{x^0-y^0}$ determines the branch that we take when using the residue theorem on the integral over $dp^0$, which results in the Heaviside step functions. Let's quickly verify this. We can rewrite as

$$\begin{aligned}
D(z) &= \int \frac{d^3 p}{(2\pi)^3}e^{i\bm p \cdot \bm z} \int \frac{dp^0}{2\pi} \frac{i}{p^0^2 - \bm p^2 - m^2 + i \epsilon} e^{-i p^0 z^0}\\
&= \int \frac{d^3 p}{(2\pi)^3}e^{i\bm p \cdot \bm z} \int \frac{dp^0}{2\pi} \frac{i}{p^0^2 - \omega_{\bm p}^2 + i \epsilon} e^{-i p^0 z^0}\\
&= \int \frac{d^3 p}{(2\pi)^3}e^{i\bm p \cdot \bm z} \int \frac{dp^0}{2\pi} \frac{i}{(p^0 - \omega_{\bm p})(p^0 + \omega_{\bm p}) + i \epsilon} e^{-i p^0 z^0}.
\end{aligned}$$

The poles are then at $p^0 = \pm \omega_{\bm p} \mp i \epsilon / (2 \omega_{\bm p}) + \bigO(\epsilon^2)$. Let's just relabel $\epsilon / (2 \omega_{\bm p}) \to \epsilon$ since we're taking $\epsilon\to 0$ anyways. When $z^0 > 0$, we choose the contour going in the lower half plane, which picks out the pole $p^0 = \omega_{\bm p} - i\epsilon$, and the $e^{-\epsilon z^0}$ ensures that the closed loop integral along the contour is equal to the integral along the real axis. Then the residue theorem gives us

$$\begin{aligned}
D(z) &= \int \frac{d^3 p}{(2\pi)^3}e^{i\bm p \cdot \bm z} \frac{-2 \pi i}{2\pi} \frac{i}{p^0 + \omega_{\bm p}} e^{-i p^0 z^0} \bigg\vert_{p^0 = \omega_{\bm p} - i\epsilon}\\
&= \int \frac{d^3 p}{(2\pi)^3}e^{i\bm p \cdot \bm z} \frac{1}{2\omega_{\bm p}} e^{-i z^0 \omega_{\bm p}}e^{- \epsilon z^0}\\
&= \int \frac{d^3 p}{(2\pi)^3}\frac{1}{2\omega_{\bm p}}e^{-i p_\mu x^\mu}.
\end{aligned}$$

Note that the minus sign on the first line (i.e. $-2\pi i$) comes from the fact that the residue theorem applies for counterclockwise contours around a polse, whereas our integral is going clockwise. When $z^0 < 0$, we choose the contour going in the upper half plane, which picks out the pole $p^0 = -\omega_{\bm p} + i\epsilon$, and the $e^{\epsilon z^0}$ ensures that the closed loop integral along the contour is equal to the integral along the real axis. Then the residue theorem gives us

$$\begin{aligned}
D(z) &= \int \frac{d^3 p}{(2\pi)^3}e^{i\bm p \cdot \bm z} \frac{2 \pi i}{2\pi} \frac{i}{p^0 - \omega_{\bm p}} e^{-i p^0 z^0} \bigg\vert_{p^0 = -\omega_{\bm p} + i\epsilon}\\
&= \int \frac{d^3 p}{(2\pi)^3}e^{i\bm p \cdot \bm z} \frac{1}{2\omega_{\bm p}} e^{i z^0 \omega_{\bm p}}e^{ \epsilon z^0}\\
&= \int \frac{d^3 p}{(2\pi)^3}\frac{1}{2\omega_{\bm p}}e^{i p_\mu x^\mu}
\end{aligned}$$

Putting this together, we find that

$$D(z) = \int \frac{d^3 p}{(2\pi)^3}\frac{1}{2\omega_{\bm p}}\parentheses{\Theta(z^0)e^{-i p_\mu x^\mu} + \Theta(-z^0) e^{i p_\mu x^\mu} }$$

as desired.



{% include post-footer.html %}
