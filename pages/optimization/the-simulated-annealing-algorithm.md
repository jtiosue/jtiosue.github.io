---
title: The simulated annealing algorithm
comments: 4
---

{% include post-header.md %}

(21 Jan 2021) (Copied from my notes from a long time ago) Simulated annealing is a specific application of the Metropolis-Hastings algorithm. I will use quantum notation here, with density matrices and Dirac notation. This is probably more complicated than it should be, but I already had it wrote up this way for some reason.

**Define**:
- $$\tau, N \in \ZZ^+$$,
- $$T \in \RR_{> 0}^{\tau}$$ (i.e. $$\forall t \in \{0, \dots, \tau-1 \}: \ T_t\in \RR_{> 0}$$),
- $$\mathcal H = \left(\mathbb C^{N}, \braket{\cdot}{\cdot} \right)$$ is an $$N$$-dimensional Hilbert space,
- $$H: \mathcal H \to \mathcal H$$ with $$H^{\dag} = H$$ is the Hamiltonian of interest,
- $$\{\ket{i}~\mid~i\in\{0, \dots, N-1\} \}$$ are orthonormal eigenvectors of $$H$$, thus an orthonormal basis of $$\mathcal H$$,
- $$H_{ii} = \bra{i} H \ket{i}$$,
- $$\forall i, j, t: \ p_{ij}^t \in [0, 1]$$ with $$\forall i, t: \ \sum_{j}p_{ij}^t = 1$$; $$p_{ij}^t$$ represents the probability of going from state $$\ket i$$ to state $$\ket j$$ at step $$t$$,
- $$\rho^0 : \mathcal H \to \mathcal H$$ is a positive semi-definite operator with $$\tr \rho^0 = 1$$ representing the initial quantum state,
- $$K_{ij}^t = \sqrt{p_{ij}^t} \ketbra{j}{i}$$; the set $$\{K_{ij}^t \}$$ forms a valid set of Krauss operators since $$\sum_{i,j} K_{ij}^{t\dag} K_{ij}^t = \II_N$$,
- $$\mathcal E^t: \rho \mapsto \sum_{i, j} K_{ij}^t \rho K_{ij}^{t\dag}$$ is the quantum channel at step $$t$$,
- $$\rho^{t+1} = \mathcal E^t\left(\rho^t \right)$$ is a simulated annealing step, and
- $$\rho^\tau$$ is the final state of the system.

If $$\rho$$ is the state that we are trying to achieve, then we want it to be a fixed point of the quantum operation: $$\rho^t = \mathcal E^t\left(\rho^t\right)$$. Plugging in and simplifying this expression we find that $$\rho^t$$ is a fixed point if

$$\sum_i \sum_{j\neq i} p_{ij}^t \bra{i}\rho^t \ket{i} \left(\ketbra{j}{j} - \ketbra{i}{i} \right) = 0.$$

Contracting, this yields the **detailed balance** condition,

$$\forall x:~~\sum_{i\neq x} p_{ix}^t \bra{i}\rho^t \ket{i} = \bra{x}\rho^t \ket{x}\sum_{i\neq x}p_{xi}^t.$$

Consider that our desired final state is $$\rho^t \propto e^{-H / T_t}$$ (e.g. the Boltzmann distribution). Then it is easy to see by plugging in that

$$p_{ij}^t = \begin{cases}
    \frac{1}{N}\exp\left(-\frac{\max \left\{0, H_{jj}-H_{ii} \right\}}{T_t} \right)&{\text{if }i \neq j},\\
    1 - \sum_{k \neq i}^{N-1}p_{ik}^t&{\text{if }i = j}.
\end{cases}$$

satisfies the detailed balance condition, and therefore the Boltzmann distribution is a fixed state of the simulated annealing algorithm. Proving that it is the *only* fixed state and that it will be reached regardless of the initial state involves using the *Ergodicity Theorem* (I think) (and I'm not even positive if that is the case). But assuming this is the case, then $$\exists \tau, T$$ such that the simulated annealing algorithm will create the Boltzmann distribution. To minimize a function, then, we want to slowly lower the temperature $$T_t$$. In practice, generally a geometric schedule is used (why?); e.g. a schedule such that $$T_{t+1} / T_t = r$$ for some constant $$r \in (0, 1)$$. In practice, the $$p_{ij}^t$$ from above is not used, because it would require computing all $$N$$ eigenvalues of $$H$$ at each step.

One could aso do something like the following, though it is probably not a great choice unless you somehow use good information to choose $$G$$.

$$p_{ij}^t = \begin{cases}
    \exp\left(-\frac{\max\{0, H_{jj}-H_{ii} \}}{T_t} \right)&\text{if }j = G(i),\\
    1-p_{i,G(i)}^t&\text{if }i = j,\\
    0&\text{else},
\end{cases}$$

where $$G: \{0,\dots, N-1\} \to \{0, \dots, N-1 \}$$ defines a bijection. Proving the uniqueness of the fixed point for these $$p_{ij}^t$$ is straightforward. Plugging into the detailed balance condition and simplifying, we can get rid of the $$\max$$ expressions and we are left with the condition that the fixed point for this system satisfies

$$\forall x:~~\frac{\bra{G(x)}\rho^t \ket{G(x)}}{\bra{x}\rho^t \ket{x}} = \exp\left(-\frac{H_{G(x), G(x)} - H_{x,x}}{T_t} \right),$$

and by using a sort of recursive relation with the bijection, this becomes equivalent to

$$\forall i, j:~~\frac{\bra{i}\rho^t \ket{i}}{\bra{j}\rho^t \ket{j}} = \exp\left(-\frac{H_{ii} - H_{jj}}{T_t} \right),$$

which is precisely the definition of the Boltzmann distribution. Because $$G$$ is a bijection, no matter what the initial state, if we simulate for long enough there is a nonzero probability to be in all other states. Therefore, no matter what the initial state, we will definitely end up in the Boltzmann distribution if we simulate for long enough.


### Algorithm in practice

Consider annealing a spin-1/2 Hamiltonian $$H$$ represented by the energy function $$E(z) = \sum_{i=0}^{n-1} h_i z_i + \sum_{i < j} J_{ij}z_i z_j + \dots$$, where $$2^n = N$$ and $$z \in \{1, -1 \}^n$$. A common implementation (see for example [qubovert](https://github.com/jtiosue/qubovert/tree/master/qubovert/sim) or [dwave-neal](https://github.com/dwavesystems/dwave-neal/)) of simulated annealing is as follows.


- *Input*
  - $$E: \{1, -1 \}^n \to \mathbb R$$;
  - $$z^0 \in \{1, -1 \}^n$$;
  - $$\tau \in \mathbb Z^+$$;
  - $$T \in \mathbb R_{>0}^\tau$$;
- *Steps*
  - $$z \leftarrow z^0$$;
  - For $$t=0,\dots,\tau-1$$;
    - For $$s=0,\dots,n-1$$;
      - $$h \stackrel{\textrm{uniform}}{\sim} \{0, \dots, n-1 \}$$;
      - $$z' \leftarrow z$$ but with the spin $$h$$ flipped;
      - $$u \stackrel{\textrm{uniform}}{\sim} [0, 1]$$;
      - If $$u < \exp\left(-\frac{\max\{0, E(z) - E(z') \}}{T_t}\right)$$;
        - $$z \leftarrow z'$$;
- *Output*
  - $$z \in \{1, -1 \}^n$$.


{% include post-footer.html %}
