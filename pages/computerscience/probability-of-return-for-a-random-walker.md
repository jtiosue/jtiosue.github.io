---
title: Probability of return for a random walker
comments: 20
---

{% include post-header.md %}

(13 May 2021) In this post I will *very informally* show that if a random walker walks forever in one or two dimensions, then she will *definitely* return to her starting spot at some point, whereas if a random walker walks forever in three or greater dimensions, then she may not ever return to her starting spot. The last two sections of this post are based off of notes from a lecture from Victor Galitski in PHYS 625 as the University of Maryland, Spring 2021.


### Informal derivation of the diffusion equation

Let $\rho(x, t)$ denote the density of a gas in one dimension at the point $x$ at time $t$. We model diffusion as a random walk, so that the gas particles have an equal chance of moving infinitesimally to the left or right at every point. Thus, particles at the point $x-dx$ walk to both $x-2dx$ and $x$, particles at the point $x+dx$ walk to both $x+2dx$ and $x$, and particles at the point $x$ walk to both $x-dx$ and $x+dx$. In this way, the density at a point $x$ at time $t+dt$ is simply the density coming from the points $x\pm dx$,

$$\rho(x, t+dt) = \frac{1}{2}\rho(x-dx,t) + \frac{1}{2}\rho(x+dx, t).$$

We note that in this informal derivation, $dt$ represents some characteristic small timescale with which jumps happen. Therefore,

$$\begin{aligned}
\rho(x, t) + \partial_t\rho(x,t)dt + \bigO{dt^2} &= \frac{1}{2}\parentheses{\rho(x,t) - \partial_x \rho(x,t)dx + \frac{1}{2}\partial_x^2 \rho(x,t) dx^2 + \bigO{dx^3}}\\
&\qquad + \frac{1}{2}\parentheses{\rho(x,t) + \partial_x \rho(x,t)dx + \frac{1}{2}\partial_x^2 \rho(x,t) dx^2 + \bigO{dx^3}}\\
&= \frac{1}{2}\partial_x^2 \rho(x,t)dx^2 + \rho(x, t) + \bigO{dx^3}.
\end{aligned}$$

Thus we have that

$$\partial_t \rho(x,t) = \frac{dx^2}{2dt}\partial_x^2 \rho(x,t).$$

Call the proportionality factor $D = \frac{dx^2}{2dt}$, so that

$$\partial_t \rho(x, t) = D \partial_x^2 \rho(x, t).$$

More generally, one can imagine jumps of size $\delta$ that occur accoringing to some probability density function $p(\delta)$. In this case, the analysis is the same, but we'd find that

$$D = \int_{-\infty}^\infty \frac{\delta^2}{2dt}\cdot p(\delta) d\delta.$$

One can of course generalize all of this to higher dimensions $d$, where the diffusion equation then takes the form

$$\partial_t \rho(\bm r, t) = D \nabla^2 \rho(\bm r, t).$$


### Diffusion equation Green's function

Consider a function $G(\bm r, t; \bm r', t)$ that satisfies

$$\parentheses{\partial_t - D \nabla^2} G(\bm r, t; \bm r', t) = \delta^d(\bm r - \bm r')\delta(t - t').$$

Such a function is called a *Green's function* because it satisfies

$$\begin{aligned}
  \parentheses{\partial_t - D \nabla^2}\int d^d r' G(\bm r, t; \bm r', t')\rho(\bm r', t') &= \int d^d r' \delta^d(\bm r - \bm r')\delta(t-t')\rho(\bm r', t')\\
  &= \delta(t-t')\rho(\bm r, t),
\end{aligned}$$ 

which equals zero whenver $t \neq t'$. Thus, if $\rho(\bm r', 0)$ is a solution at time $t=0$, then

$$\rho(\bm r, t) = \int d^d r' ~ G(\bm r, t; \bm r', 0) \rho(\bm r', 0)$$

is a solution at time $t$. Thus $G(\bm r, t; \bm r', 0)$ tells us something about the probability to transition from $\bm r'$ to $\bm r$ in a time $t$. In particular, suppose we are initially localized at zero, which corresponds to $\rho(\bm r',0) = \delta^d(r')$, where $\delta^d$ is the $d$-dimensional Delta (generalized) function. Then $\rho(\bm r, t) = G(\bm r, t; \bm 0, 0)$. Therefore, if we start off completely localized at zero, then the probability that we are localized somewhere within a distance $\epsilon$ from zero at time $t$ is $\int_{\abs{\bm r} < \epsilon} d^d r~ G(\bm r, t)$, where we define $G(\bm r, t) = G(\bm r, t; \bm 0, 0)$. 

By going to Fourier space, the equation for the Green's function becomes

$$\parentheses{-i\omega + D p^2} G(\bm p, \omega) = 1$$

where now $\omega$ corresponds to $t-t'$ and $\bm p$ to $\bm r - \bm r'$. Thus,

$$G(\bm r, t) = \int \frac{d^dp}{(2\pi)^d} \frac{d\omega}{2\pi} \exp\pargs{i\omega t - i\bm p \cdot \bm r}\frac{1}{(-i\omega + D p^2)}.$$

Going through this integral, one finds that $G(0, t) \propto t^{-d/2}$.


### Probability of return

As we informally argued before, if we start off completely localized at zero, then the probability that we are localized somewhere within a distance $\epsilon$ from zero at time $t$ is $\int_{\abs{\bm r} < \epsilon} d^d r~ G(\bm r, t)$. For small epsilon, this is $\approx G(0,t) \frac{\pi^{d/2} \epsilon^d}{\Gamma(1+d/2)}$. The last factor comes from the volume of the $d$-ball of radius $\epsilon$. 

Thus, the probability to return to the same point as we started -- i.e. zero -- at some point in the future after a time $\tau_i$, is something like

$$\begin{aligned}
\lim_{\epsilon\to 0} \epsilon^d \int_{\tau_i}^{\infty} G(0,t)dt &\propto \lim_{\epsilon\to 0} \epsilon^d\int_{\tau_i}^{\infty} t^{-d/2} dt\\
&= \lim_{\epsilon\to 0} \int_{\tau_i}^{\infty} (t/\epsilon^2)^{-d/2} dt\\
&= \lim_{\epsilon\to 0} \epsilon^2 \int_{\tau_i/\epsilon^2}^{\infty} u^{-d/2} du.
\end{aligned}$$

We see that when $d = 1$ or $2$, this integral blows up, but when $d \geq 3$, it stays finite. This is characteristic of the fact that if a random walker walks forever in one or two dimensions, then she will *definitely* return to her starting spot at some point. However, if a random walker walks forever in three or greater dimensions, then she may not ever return to her starting spot.


{% include post-footer.html %}
