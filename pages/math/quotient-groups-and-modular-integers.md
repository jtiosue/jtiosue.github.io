---
title: Quotient groups and modular integers
comments: 8
---

{% include post-header.md %}

(28 Jan 2021) Perhaps the main point of my website is to organize the many small things that I learn as I go along so that they are easily accessible for future reference. With that in mind, the purpose of this post is really only to describe the notation $$\bbZ / n \bbZ$$ for the set of integers modulo $$n$$.

First consider a group $$(A, \cdot)$$. $$B$$ is called a *normal subgroup* of $$A$$ if $$\forall a \in A$$: $$a\cdot B = B \cdot a$$. For example, $$(n\bbZ = \curlybrackets{nx ~\mid~ x \in \bbZ }, +)$$ is a normal subgroup of $$(\bbZ, +)$$ because for any $$z \in \bbZ$$, we have that $$z + n\bbZ = n\bbZ + z.$$

Given $$(A, \cdot)$$ and a normal subgroup $$B$$, the quotient group $$A/B$$ is defined by

$$A/B \coloneqq \curlybrackets{\brackets a~\mid~a \in A },$$

where $$\brackets a$$ denotes the equivalence class

$$\brackets a \coloneqq \curlybrackets{a \cdot b ~\mid~ b \in B } = a \cdot B = B \cdot a.$$

Now let's go back to our example where $$(A, \cdot) = (\bbZ, +)$$ and $$B = n \bbZ$$. For any $$z \in \bbZ$$, we have that

$$\brackets z = \curlybrackets{z + b ~\mid~ b \in n \bbZ }.$$

So, in particular,

$$\begin{aligned}
\dots &= \dots\\
\brackets 0 &= n\bbZ,\\
\brackets 1 &= 1+n\bbZ,\\
\vdots &= \vdots\\
\brackets{n-1} &= n-1+n\bbZ,\\
\brackets n &= n+n\bbZ = n\bbZ,\\
\brackets{n+1} &= n+1+n\bbZ = 1+n\bbZ,\\
\vdots &= \vdots
\end{aligned}$$

So we see that $$\brackets 0 = \brackets n$$, $$\brackets 1 = \brackets{n+1}$$, and so on. Since a set has no repeated elements, it is clear that

$$\bbZ / n\bbZ = \curlybrackets{\brackets 0, \brackets 1, \dots, \brackets{n-1} };$$

in other words, it is the set of equivalence classes of the integers modulo $$n$$. Considering $$n=2$$ as an example,

$$\bbZ / 2 \bbZ = \curlybrackets{\brackets 0, \brackets 1 },$$

or equivalently,

$$\bbZ / 2 \bbZ = \curlybrackets{\brackets 2, \brackets 3 },$$

and so on. Indeed,

$$\bbZ / 2\bbZ = \curlybrackets{0+\bbZ, 1+\bbZ}.$$

When working with the numbers modulo $$n$$, one defines an equivalence relation $$\equiv$$ that acompanies the equivalence classes $$\brackets z$$. We say that for any $$a, b \in \bbZ$$,

$$a \equiv b ~\Leftrightarrow~\brackets a = \brackets b.$$

Thus the equivalence of integers modulo $$n$$ is expressed as an equality between sets, with those sets being the equivalence classes. In the $$n=2$$ case, $$0 \equiv 2 \equiv 4$$ and so on, because $$\brackets 0 = \brackets 2 = \brackets 4$$. Oftentimes, to keep clear what equivalence relation is being used, one uses the notation $$a \equiv b \pmod n$$.

*Note*: $$a \equiv b \mod n$$ is *not the same* as $$a \equiv b \pmod n$$. In fact, the former is an invalid statement. The parentheses indicate that the modulo applies to the whole equation. $$b \mod n$$ is the *unique* integer $$z$$ that satisfies $$z \equiv b \pmod n$$ and $$0 \leq z < n$$. See [Wikipedia](https://en.wikipedia.org/wiki/Modular_arithmetic#Congruence) for more details.


## Aside on congruence relations

Technically $$\equiv$$ defines a congruence relation, which is an equivalence relation that is also compatible with multiplication, addition, and subtraction. For example, for $$a, b, c \in \bbZ$$,

$$a \equiv b ~\Rightarrow ~ a+c \equiv b+c.$$

This statement is by definition the same as

$$\brackets a = \brackets b ~\Rightarrow ~ \brackets{a+c}=\brackets{b+c},$$

which we see is obviously true. Similarly,

$$a \equiv b ~\Rightarrow ~ ca \equiv cb,$$

which is equivalent to

$$\brackets a = \brackets b ~\Rightarrow ~ \brackets{ca} = \brackets{cb},$$

which is again simple to show using the definition of $$\brackets \cdot$$.


## Aside on isomorphisms

Let's discuss $$\bbZ / 2\bbZ$$ here as an example. If we define $$\oplus$$ as addition modulo 2, so that

$$\begin{aligned}
0 \oplus 0 &= 0\\
0 \oplus 1 &= 1\\
1 \oplus 0 &= 1\\
1 \oplus 1 &= 0,
\end{aligned}$$

then $$\parentheses{\bbZ / 2\bbZ, +} \cong \parentheses{\curlybrackets{0, 1}, \oplus}$$. However, this is perhaps not the most natural isomorphism seeing as the group operation $$\oplus$$ is essentially defined such that this isomorphism exists.

Suppose we instead chose $$\phi: \bbZ / 2\bbZ \to \curlybrackets{-1, 1}$$, with $$\phi\parentheses{\brackets 0} = 1$$ and $$\phi\parentheses{\brackets 1} = -1$$. Then $$\phi$$ is a homomorphism between $$\parentheses{\bbZ / 2\bbZ, +}$$ and $$\parentheses{\curlybrackets{1, -1}, \cdot}$$.

$$\begin{aligned}
\phi\parentheses{\brackets x + \brackets y} &= \phi\parentheses{x + y + 2\bbZ}\\
&= \phi\parentheses{\brackets{x + y}}.
\end{aligned}$$

When $$x = y = 0$$, this equals $$\phi\parentheses{\brackets 0} = 1$$ which is indeed the same as $$\phi\parentheses{\brackets 0} \cdot \phi\parentheses{\brackets 0} = 1$$. When $$x = 0$$ and $$y = 1$$, this equals $$\phi\parentheses{\brackets 1} = -1$$ which is indeed the same as $$\phi\parentheses{\brackets 0} \cdot \phi\parentheses{\brackets 1} = -1$$. Similarly, one can work out the other two possiblities for $$x$$ and $$y$$. $$\phi$$ is also bijective so that it is an isomorphism.

In general, one finds an isomorphism between $$\bbZ / n\bbZ$$ and 

$$\parentheses{\curlybrackets{\exp\parentheses{2\pi i x / n}~\mid~ x \in \curlybrackets{0, \dots, n-1}}, \cdot}$$

via $$\phi: \brackets x \mapsto \exp\parentheses{2\pi i x / n}$$.


**Next example**: $$\bbR / \bbZ$$. Now Let's consider the example of $$\bbR / \bbZ$$, where again the group operation is $$+$$. Notice that

$$\begin{aligned}
\bbR / \bbZ &= \curlybrackets{r + \bbZ ~\mid~r \in \bbR}\\
&= \curlybrackets{r + \bbZ ~\mid~ r \in [0, 1)}.
\end{aligned}$$

Again it may be tempting to say that $$\bbR / \bbZ$$ is isomorphic to $$[0, 1)$$ with some suitable group operation on $$[0, 1)$$. But instead consider $$\phi: r + \bbZ \mapsto \exp(2\pi i r)$$. We see that $$\phi$$ is a homomorphism between $$\bbR/\bbZ$$ and the group $$\parentheses{S^1, \cdot}$$, e.g. the unit circle, because

$$\begin{aligned}
\phi\parentheses{\parentheses{r_1 + \bbZ} + \parentheses{r_2+\bbZ}} &= \phi\parentheses{r_1 + r_2 + \bbZ}\\
&= \exp\parentheses{2\pi i \parentheses{r_1+r_2}}\\
&= \exp\parentheses{2\pi i r_1} \cdot \exp\parentheses{2\pi i r_2}\\
&= \phi\parentheses{r_1+\bbZ}\cdot \phi\parentheses{r_2+\bbZ};
\end{aligned}$$

(alternatively, one could think of $$\phi: \bbR/ \bbZ \to U(1)$$ instead). It is straightforward to see that $$\phi$$ is both injective and surjective, and therefore is an isomorphism.


## Aside on normal subgroups

We mentioned above that a subgroup $$B \leq A$$ (the $$\leq$$ means subgroup) is a normal subgroup of $$A$$ if $$a \cdot B = B \cdot a$$ for all $$a \in A$$ (left and right *cosets* are the same). We then defined the quotient group $$A / B$$ to be the set $$\curlybrackets{a\cdot B ~\mid~ a \in A}$$. You may ask, why do we restrict our definition of the quotient group to normal subgroups? The reason is as follows.

The quotient group defines an equivalence relation $$\sim$$ (for modular integers above we used $$\equiv$$ instead of $$\sim$$) so that $$\forall a, b \in A$$, $$a \sim b$$ iff $$a \cdot B = b \cdot B$$. For the $$\cdot$$ operation to be well-defined under this equivalence relation, we want that if $$a \sim a'$$ and $$b \sim b'$$, then $$a \cdot b \sim a' \cdot b'$$. So

$$a \cdot B = a' \cdot B, b \cdot B = b' \cdot B ~\implies~ a\cdot b \cdot B = a' \cdot b' \cdot B.$$

If we require that $$B$$ is normal, then

$$\begin{aligned}
a \cdot b \cdot B &= a \cdot (B \cdot b)\\
&= a \cdot B \cdot b'\\
&= a' \cdot B \cdot b'\\
&= a' \cdot b' \cdot B.
\end{aligned}$$

So we see that requiring $$B$$ to be normal means that the operation is well-defined. Next, we will *not* assume that $$B$$ is normal. We will show that the operation being well-defined implies that $$B$$ must be normal.

Consider that $$b \in B$$, $$a \in A$$, and $$e$$ is the identity in $$A$$ and $$B$$. The multiplication happens on equivalence classes/cosets; i.e. $$\parentheses{a \cdot B} \cdot \parentheses{b \cdot B} = \parentheses{a \cdot b \cdot B}$$. Then

$$B = e \cdot B =  b\cdot B.$$

Therefore,

$$\parentheses{e \cdot B }\cdot \parentheses{a \cdot B} = \parentheses{e \cdot a} \cdot B = a \cdot B.$$

Similarly,

$$\parentheses{b \cdot B} \cdot \parentheses{a \cdot B} = \parentheses{b \cdot a} \cdot B.$$

Thus, $$a \cdot B = b \cdot a \cdot B$$, which implies that $$a^{-1} \cdot b \cdot a \cdot B = B$$. Then $$a^{-1} \cdot b \cdot a \in B$$, so that $$b \cdot a \in a \cdot B$$ and $$a^{-1} \cdot b \in B \cdot a^{-1}$$. Or, $$B \cdot a \subseteq a \cdot B$$ and $$a \cdot B \subseteq B \cdot a$$ for all $$a \in A$$ (we can get rid of the inverse by just noticing that $$\exists a' \in A$$ such that $$a^{-1} = a'$$, and then relabling $$a' \to a$$). Indeed, these two imply that $$a \cdot B = B\cdot a$$ for all $$a$$, implying that $$B$$ is indeed normal.


#### References

- [https://math.stackexchange.com/questions/14282/why-do-we-define-quotient-groups-for-normal-subgroups-only](https://math.stackexchange.com/questions/14282/why-do-we-define-quotient-groups-for-normal-subgroups-only)


{% include post-footer.html %}
