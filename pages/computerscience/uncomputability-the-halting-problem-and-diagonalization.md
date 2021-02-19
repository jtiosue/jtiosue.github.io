---
title: Uncomputability, the halting problem, and diagonalization
comments: 5
---

{% include post-header.md %}

(23 Jan 2021) (Copied from my notes from a long time ago) I'll briefly discuss diagonalization, and then apply the standard diagonalization method to the halting problem to show that the halting problem is indeed uncomputable.


### Cantor's diagonalization

**Definition**: A set in countable if either 1) the set is finite, or 2) the set shares a one-to-one correspondence with the set of positive integers $$\ZZ^+$$.

**Theorem**: The set of real numbers $$\RR$$ is not countable.

*Proof*: We will prove that the set $$(0, 1) \subset \mathbb R$$ is uncountable. First, we assume that $$(0, 1)$$ *is* countable. Then consider we list the bijection between it and $$\mathbb Z^+$$. We represent the $$i^\textrm{th}$$ element in the list in binary form as $$0.d_{i1}d_{i2}d_{i3}\dots$$, where each $$d_{ij} \in \{0, 1 \}$$.

$$\begin{aligned}
    1:& & 0.d_{11}d_{12}d_{13}d_{14}\dots\\
    2:& & 0.d_{21}d_{22}d_{23}d_{24}\dots\\
    3:& & 0.d_{31}d_{32}d_{33}d_{34}\dots\\
    \dots:& & \dots
\end{aligned}$$

Let $$\overline d = 1 - d$$, Consider the number $$0.\overline d_{11}\overline d_{22}\overline d_{33}\overline d_{44}\dots$$. This number is not in the above list. But we assumed that it was. Thus we find a contradiction. Therefore, the assumption that $$(0, 1)$$ is countable is false, proving the theorem. {% include endproof.html %}


### The halting problem

Let $$\mathcal M = \{M_i ~\mid~ i \in \ZZ^+ \}$$, where each $$M_i$$ is a Turing machine that solves a problem. $$M_i$$ on input $$x$$ can

1. Loop forever,
2. return "Y" = "Yes",
3. return "N" = "No", or
4. return something else (not important).

Let

$$A = \{\langle M, x \rangle ~\mid~ M \in \mathcal{M} ~ \textrm{s.t.} ~ M(x) = \textrm{Y} \},$$ 

where $$\langle \cdot \rangle$$ denotes a description (i.e. $$\langle M, x \rangle$$ is a description of the Turing machine $$M$$ and the input $$x$$). In words, $$A$$ is the set of all (machine, input) pairs where the machine returns Yes on the input. 

We claim that $$A$$ is uncomputable, meaning that $$\nexists M_A$$ s.t. $$M_A\left(\langle M, x \rangle \right) =$$ Y iff $$\langle M, x \rangle \in A$$ and $$M_A\left(\langle M, x \rangle \right) =$$ N iff $$\langle M, x \rangle \notin A$$. We note that $$\langle M, x\rangle$$ is just some description of the machine and input (ie maybe a binary description). Thus, there does not exist a Turing machine (or in more modern terms, there does not exist a program) that can determine if an arbitrary Turing machine (program) halts on an input.

**Theorem**: $$A$$ is uncomputable.

*Proof*: Assume $$\exists M_A \in \mathcal M$$ that can compute if an arbitrary $$\langle M, x \rangle$$ pair belongs in $$A$$. We will prove that this causes a contradiction. 

Construct a machine variant $$D$$. Recall that $$\langle M \rangle$$ for $$M \in \mathcal M$$ is just some description of the machine (program). $$D$$ on input $$\langle M \rangle$$ is defined as

$$D(\langle M \rangle) = \overline{M_A\left(\langle M, \langle M \rangle \rangle \right)}.$$

In other words $$D$$ on input $$\langle M \rangle$$ disagrees with $$M_A$$ on input $$\langle M , \langle M \rangle \rangle$$. Let's run $$D$$ on the description of itself $$\langle D \rangle$$.

$$D(\langle D \rangle) =$$
- Yes $$\leftrightarrow M_A(\langle D, \langle D \rangle \rangle) =$$ N $$\leftrightarrow \langle D, \langle D \rangle \rangle \notin A$$.
- No $$\leftrightarrow M_A(\langle D, \langle D \rangle \rangle) =$$ Y $$\leftrightarrow \langle D, \langle D \rangle \rangle \in A$$.

We see the second bullet is very clearly a contradiction, because it is saying that if $$D(\langle D \rangle) =$$ N, then $$\langle D, \langle D \rangle \rangle \in A$$, meaning that $$D(\langle D \rangle) =$$ Y.

We encountered a contradiction, meaning that one of our assumptions must be false. I am told that there are some subtleties that this proof overlooks (though I don't see them personally), but basically the only assumption that could be false is the assumption that $$M_A$$ exists. {% include endproof.html %}

#### Relation to diagonalization

This proof using "diagonalization" because we basically construct the following table, where the machines are along the first row and the inputs are along the first column, and find problems along the diagonal.

$$\begin{array}{c|cccc}
& M_1 & M_2 & M_3 & \dots \\
\hline
\langle M_1 \rangle & \textrm{Y} & \infty & \textrm{Y} & \dots \\
\langle M_2 \rangle & \textrm{Y} & \textrm{N} & \textrm{N} & \dots \\
\langle M_3 \rangle & \textrm{N} & \textrm{Y} & \infty & \dots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{array}$$

{% include post-footer.html %}
