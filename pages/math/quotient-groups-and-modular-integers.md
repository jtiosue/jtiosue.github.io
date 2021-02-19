---
title: Quotient groups and modular integers
comments: 8
---

{% include post-header.md %}

(28 Jan 2021) Perhaps the main point of my website is to organize the many small things that I learn as I go along so that they are easily accessible for future reference. With that in mind, the purpose of this post is really only to describe the notation $$\ZZ / n \ZZ$$ for the set of integers modulo $$n$$.

First consider a group $$(A, \cdot)$$. $$B$$ is called a *normal subgroup* of $$A$$ if $$\forall a \in A$$: $$a\cdot B = B \cdot a$$. For example, $$(n\ZZ = \braces{nx ~\mid~ x \in \ZZ }, +)$$ is a normal subgroup of $$(\ZZ, +)$$ because for any $$z \in \ZZ$$, we have that $$z + n\ZZ = n\ZZ + z.$$

Given $$(A, \cdot)$$ and a normal subgroup $$B$$, the quotient group $$A/B$$ is defined by

$$A/B \coloneqq \braces{\brackets a~\mid~a \in A },$$

where $$\brackets a$$ denotes the equivalence class

$$\brackets a \coloneqq \braces{a \cdot b ~\mid~ b \in B }.$$

Now let's go back to our example where $$(A, \cdot) = (\ZZ, +)$$ and $$B = n \ZZ$$. For any $$z \in \ZZ$$, we have that

$$\brackets z = \braces{z + b ~\mid~ b \in n \ZZ }.$$

So, in particular,

$$\begin{aligned}
\dots &= \dots\\
\brackets 0 &= n\ZZ,\\
\brackets 1 &= 1+n\ZZ,\\
\vdots &= \vdots\\
\brackets{n-1} &= n-1+n\ZZ,\\
\brackets n &= n+n\ZZ = n\ZZ,\\
\brackets{n+1} &= n+1+n\ZZ = 1+n\ZZ,\\
\vdots &= \vdots
\end{aligned}$$

So we see that $$\brackets 0 = \brackets n$$, $$\brackets 1 = \brackets{n+1}$$, and so on. Since a set has no repeated elements, it is clear that

$$\ZZ / n\ZZ = \braces{\brackets 0, \brackets 1, \dots, \brackets{n-1} };$$

in other words, it is the set of equivalence classes of the integers modulo $$n$$. Considering $$n=2$$ as an example,

$$\ZZ / 2 \ZZ = \braces{\brackets 0, \brackets 1 },$$

or equivalently,

$$\ZZ / 2 \ZZ = \braces{\brackets 2, \brackets 3 },$$

and so on. Indeed,

$$\ZZ / 2\ZZ = \braces{0+\ZZ, 1+\ZZ}.$$

When working with the numbers modulo $$n$$, one defines an equivalence relation $$\equiv$$ that acompanies the equivalence classes $$\brackets z$$. We say that for any $$a, b \in \ZZ$$,

$$a \equiv b ~\Leftrightarrow~\brackets a = \brackets b.$$

Thus the equivalence of integers modulo $$n$$ is expressed as an equality between sets, with those sets being the equivalence classes. In the $$n=2$$ case, $$0 \equiv 2 \equiv 4$$ and so on, because $$\brackets 0 = \brackets 2 = \brackets 4$$. Oftentimes, to keep clear what equivalence relation is being used, one uses the notation $$a \equiv b \pmod n$$.

*Note*: $$a \equiv b \mod n$$ is *not the same* as $$a \equiv b \pmod n$$. In fact, the former is an invalid statement. The parentheses indicate that the modulo applies to the whole equation. $$b \mod n$$ is the *unique* integer $$z$$ that satisfies $$z \equiv b \pmod n$$ and $$0 \leq z < n$$. See [Wikipedia](https://en.wikipedia.org/wiki/Modular_arithmetic#Congruence) for more details.


## Aside on congruence relations

Technically $$\equiv$$ defines a congruence relation, which is an equivalence relation that is also compatible with multiplication, addition, and subtraction. For example, for $$a, b, c \in \ZZ$$,

$$a \equiv b ~\Rightarrow ~ a+c \equiv b+c.$$

This statement is by definition the same as

$$\brackets a = \brackets b ~\Rightarrow ~ \brackets{a+c}=\brackets{b+c},$$

which we see is obviously true. Similarly,

$$a \equiv b ~\Rightarrow ~ ca \equiv cb,$$

which is equivalent to

$$\brackets a = \brackets b ~\Rightarrow ~ \brackets{ca} = \brackets{cb},$$

which is again simple to show using the definition of $$\brackets \cdot$$.


## Aside on isomorphisms

Let's discuss $$\ZZ / 2\ZZ$$ here as an example. If we define $$\oplus$$ as addition modulo 2, so that

$$\begin{aligned}
0 \oplus 0 &= 0\\
0 \oplus 1 &= 1\\
1 \oplus 0 &= 1\\
1 \oplus 1 &= 0,
\end{aligned}$$

then $$\parentheses{\ZZ / 2\ZZ, +} \cong \parentheses{\braces{0, 1}, \oplus}$$. However, this is perhaps not the most natural isomorphism seeing as the group operation $$\oplus$$ is essentially defined such that this isomorphism exists.

Suppose we instead chose $$\phi: \ZZ / 2\ZZ \to \braces{-1, 1}$$, with $$\phi\parentheses{\brackets 0} = 1$$ and $$\phi\parentheses{\brackets 1} = -1$$. Then $$\phi$$ is a homomorphism between $$\parentheses{\ZZ / 2\ZZ, +}$$ and $$\parentheses{\braces{1, -1}, \cdot}$$.

$$\begin{aligned}
\phi\parentheses{\brackets x + \brackets y} &= \phi\parentheses{x + y + 2\ZZ}\\
&= \phi\parentheses{\brackets{x + y}}.
\end{aligned}$$

When $$x = y = 0$$, this equals $$\phi\parentheses{\brackets 0} = 1$$ which is indeed the same as $$\phi\parentheses{\brackets 0} \cdot \phi\parentheses{\brackets 0} = 1$$. When $$x = 0$$ and $$y = 1$$, this equals $$\phi\parentheses{\brackets 1} = -1$$ which is indeed the same as $$\phi\parentheses{\brackets 0} \cdot \phi\parentheses{\brackets 1} = -1$$. Similarly, one can work out the other two possiblities for $$x$$ and $$y$$. $$\phi$$ is also bijective so that it is an isomorphism.

In general, one finds an isomorphism between $$\ZZ / n\ZZ$$ and 

$$\parentheses{\braces{\exp\parentheses{2\pi i x / n}~\mid~ x \in \braces{0, \dots, n-1}}, \cdot}$$

via $$\phi: \brackets x \mapsto \exp\parentheses{2\pi i x / n}$$.


**Next example**: $$\RR / \ZZ$$. Now Let's consider the example of $$\RR / \ZZ$$, where again the group operation is $$+$$. Notice that

$$\begin{aligned}
\RR / \ZZ &= \braces{r + \ZZ ~\mid~r \in \RR}\\
&= \braces{r + \ZZ ~\mid~ r \in [0, 1)}.
\end{aligned}$$

Again it may be tempting to say that $$\RR / \ZZ$$ is isomorphic to $$[0, 1)$$ with some suitable group operation on $$[0, 1)$$. But instead consider $$\phi: r + \ZZ \mapsto \exp(2\pi i r)$$. We see that $$\phi$$ is a homomorphism between $$\RR/\ZZ$$ and the group $$\parentheses{S^1, \cdot}$$, e.g. the unit circle, because

$$\begin{aligned}
\phi\parentheses{\parentheses{r_1 + \ZZ} + \parentheses{r_2+\ZZ}} &= \phi\parentheses{r_1 + r_2 + \ZZ}\\
&= \exp\parentheses{2\pi i \parentheses{r_1+r_2}}\\
&= \exp\parentheses{2\pi i r_1} \cdot \exp\parentheses{2\pi i r_2}\\
&= \phi\parentheses{r_1+\ZZ}\cdot \phi\parentheses{r_2+\ZZ};
\end{aligned}$$

(alternatively, one could think of $$\phi: \RR/ \ZZ \to U(1)$$ instead). It is straightforward to see that $$\phi$$ is both injective and surjective, and therefore is an isomorphism.


{% include post-footer.html %}
