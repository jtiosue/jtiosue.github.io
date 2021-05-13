---
title: Compactness on topological spaces and why it is important
comments: 11
---

{% include post-header.md %}

(07 Feb 2021) Compactness confused me for a while. Specifically, I found it difficult to gain any intuition for it due to my inability to understand the strange definition of compactness. The intuition I was always given was that compactness was somehow a generalization of finiteness; for example, [this post](https://math.stackexchange.com/a/485876/395731) says that "compactness does for continuous functions what finiteness does for functions in general". However, I failed to see how such a intuition motivates the definition. It was [this Reddit comment](https://www.reddit.com/r/math/comments/lbldwt/compactness/glvm6ld?utm_source=share&utm_medium=web2x&context=3) that finally helped me to gain some intuition for the definition.

Here I will *briefly* go over the basics of topological spaces, including how continuous functions are defined on topological spaces. Then, I'll introduce compactness and discuss the new intuition that I've learned from the Reddit post I mentioned above, followed by some results about how continuous functions interact with compact sets. I'll conclude with a theorem that seems to be a useful application of compactness.


**Notation**:
- On a metric space $(X, d)$, the open ball of radius $r\geq 0$ around the point $x \in X$ is 

$$B_r(x) \coloneqq \curlybrackets{y \in X ~\mid~ d(x, y) < r}.$$

- A subset $K \subseteq X$ is called *open* if for every point $x \in K$, there exists an $r > 0$ such that $B_r(x) \subseteq K$.
- Fix a function $f: X \to Y$, and subsets $J \subseteq X$, $Y \subseteq K$. The *image* of $J$ under $f$ is 

$$f[J] \coloneqq \curlybrackets{f(x) ~\mid~ x \in J}.$$

- The *preimage* of $K$ under $f$ is

$$f^{-1}[K] \coloneqq \curlybrackets{x \in X ~\mid~ f(x) \in K}.$$

- $\delta_{xy}$ is the Kroneker delta that equals 1 if $x = y$ and 0 otherwise.


## Overview of topological spaces, open sets, and homemorphisms

When I first began learning about topological spaces, I was very confused during my first reading over the chapter because I didn't realize that an "open set" in a topological space is different from an "open set" in a metric space. Indeed, a "topology" on a set $X$ is a *definition* of the open sets in $X$. My intuition is that these open sets define a *neighborhood structure* of your set, whereas in a metric space distances define a neighborhood structure (of course, if we make a topology with the open sets as they are defined in a metric space, then the neighborhood structure is indeed encoded in the topology). Why are they "open sets"? Recall the definition of an open set in a metric space is that there is an open ball around every point in the set. In this way, an open set is one where there is "neighborhood" around every point in the set.

**Definition**: Let $X$ be a set, and $T$ a collection of subsets of $X$ (called *open sets*), $(X, T)$ is a *topological space*. $T$ is called the *topology* of $X$, and $T$ *defines* which subsets are open. $T$ as a topology must satisfy

1. $\emptyset, X \in T$,
2. if $G_\alpha \in T$ for $\alpha \in A$, then $\bigcup_{\alpha \in A}G_\alpha \in T$ (arbitrary union),
3. if $G_i \in T$ for $i=1,\dots, n$, then $\bigcap_{i=1}^n G_i \in T$ (finite intersections).

Why does condition 3 restrict to finite intersections, whereas condition 2 allows arbitrary unions? Consider $\bbR$ with a topology defined by the Euclidean metric. That is, the opens sets are defined as subsets of the form $(a, b)$. Indeed, any finite intersection of sets of these form will also be of this form. But consider

$$\parentheses{\bigcap_{x=1}^\infty \parentheses{-1, 1/x}} \cap \parentheses{\bigcap_{x=1}^\infty \parentheses{-1/x, 1}} = \curlybrackets 0.$$

This is a non-finite intersection of open subsets, and it equals $\curlybrackets 0$, which is clearly not an open set because it is not of the form $(a, b)$. So we see that in order to recreate the notion of open sets that we are used to, we must only require finite intersections of open sets to be open.

*More to come in this section.*


#### Homeomorphisms

A homeomorphism is an isomorphism between topological spaces. This means that it is a bijective continuous function between two topological spaces whose inverse is also continuous. The fact that it is continuous implies that it prerserves the open set structure. So two spaces are homeomorphic if they are topologically equivalent.

*More to come in this section.*


### Continuity on topological spaces

What's so cool about a topological spaces is that it gives you the ability to define so many cool things based only on a definition of what open sets are. Here, for example, we can see how to define continuity of a map between topological spaces based solely on the open set structure.


**Definition**: Let $(X, T)$ be a topological space. A set $V \subseteq X$ is called a *neighborhood* of a point $x \in X$ if there exists an open set $G \in T$ such that $x \in G$ and $G \subseteq V$. Note that $V$ itself does not have to be open.

So we say $V$ is a neighborhood of $x$ if it contains an open set that contains $x$.


**Definition**: A function $f: X \to Y$ is *continuous* at a point $x \in X$ if for each neighborhood $W$ of $f(x)$ there exists a neighborhood $V$ of $x$ such that the image $f[V] \subseteq W$. $f$ is continuous if it is continuous at every $x \in X$.

We are essentially saying that for every neighborhood of a point $f(x)$ in $Y$, there is a corresponding neighborhood of the point $x$ in $X$ so that the image of $V$ is at least as small as $W$. In this way, we can continuously shrink the size of our neighborhood $W$, and be guarenteed that our neighborhood $V$ will also shrink. In othe works, very small perturbations in the range, e.g. $f(x) + \epsilon'$, correspond to very small perturbations in the domain, e.g. $f(x+\epsilon) = f(x) + \epsilon'$.

Now we show a theorem that is used as an alternative definition of continuity.

**Theorem 1**: Let $(X, T)$ and $(Y, S)$ be two topological spaces and $f: X \to Y$. Then $f$ is continuous if and only if $f^{-1}[G] \in T$ for every $G \in S$. In other words, under a continuous function the preimage of open sets is open.

*Proof*: We are really essentially only saying that the preimage of a neighborhood of $f(x)$ is a neighborhood of $x$, which is more or less our original defintion of continuity. I may come back a prove this more rigorously later, but for now see here for a proof [here](https://ece.iisc.ac.in/~parimal/proofs/lecture-17.pdf). {% include endproof.html %}


We'll conclude our discussion of continuous maps with a brief lemma that will be used later on in this post.

**Lemma 1**: Consider a continuous mapping $f: X \to Y$ for two metric spaces $X, Y$. Then for every closed set $K \subseteq Y$, the preimage $f^{-1}[K] \subseteq X$ is closed.

*Proof*: Since $K$ is closed, $Y\setminus K$ is open. We saw in the theorems above that for a continuous function, the preimage of open sets is open. Therefore, $f^{-1}[Y\setminus K]$ is open. Then,

$$f^{-1}[Y\setminus K] = f^{-1}[Y]\setminus f^{-1}[K] = X\setminus f^{-1}[K]$$

is open, so $f^{-1}[K]$ is closed. {% include endproof.html %}


## Compactness

**Definition**: A subset $K$ of a topological space $(X, T)$ is *compact* if every open cover of $K$ contains a finite subcover.

**Example**: Consider the metric space $(\bbR, d)$ where $d$ is the standard Euclidean metric. This induces a topology so that open sets are of the form $(a, b) \subseteq \bbR$. The subset $(0, 1)$ is covered by the open sets $\curlybrackets{(0, 1-1/n)~\mid~ n \in \bbN}$. However, any finite subset of these does not cover $(0, 1)$. Therefore, $(0, 1)$ with this topology is not compact. However, $[0, 1]$ *is* compact.

**Example**: Consider the metric space $(\bbR, d)$ where $d$ is the discrete metric defined

$$\begin{aligned}
d: &~\bbR \times \bbR \to [0, \infty)\\
&~(x, y) \mapsto 1-\delta_{xy}.
\end{aligned}$$

This metric induces a discrete topology, so that every subset of $\bbR$ is defined as an open set. In this case, even the subset $[0, 1]$ is not compact. Consider the open cover 

$$\curlybrackets{\curlybrackets{k} ~\mid~ k\in [0, 1]}.$$

Such a cover is open because $\curlybrackets{k}$ is open, and it cannot be made finite. We can easily see then that a subset is compact only if it is finite; e.g. $\curlybrackets{\curlybrackets 0, \curlybrackets 1}$ is compact.


#### Where does this definition come from?

The "open cover" definition of a compact set is intuitively a topologically invariant way of describing a bounded set. For example, consider $\bbR$ with the Euclidean metric $d$. The subset $(0, 1)$ is bounded. But it is homeomorphic to $(-\infty, \infty) = \bbR$ via the function $f(x) = 1/(1-x) - 1/x$. Indeed $\bbR$ is unbounded. Homeomorphic spaces are indistiguishable as topological spaces since a homeomorphism preserves topology. Clearly, then, *boundedness* is not a topological invariant. We showed in our example above that $(0, 1)$ is not compact.

So how do we describe "boundedness" (and completeness) in a topologically invariant way? All statements in topology are about open sets, since that's what a topology *is*. So consider making a measuring stick on a topological space. It must be made out of open sets. Let's say our measuring stick is a collection of open sets $(n, n+2)$ for $n \in \bbZ$. We need infinitely many of these to cover the whole real line.

Measuring in this way is topologically invariant. If you have a homeomorphism, all the open sets get adjusted along with the set. With a homeomorphism from $\bbR$ to $(0, 1)$, all our measuring sticks get squeezed so that $(0, 1)$ is still unbounded. With this topologically invariant way of describing boundedness (and completeness), we can say that a compact set is one where no matter how you cover your set with measuring sticks/open sets, you could do just as well with finitely many of them.


### Image of compact sets via continuous functions are compact

The following theorem shows that compactness is a continuous invariant. In some sense compactness plays nicely with continuous functions, and this is part of what makes compactness so important.

**Theorem 2**: Let $T_1, T_2$ be two topological spaces with their own respective topologies. Let $f: T_1 \to T_2$ be a continuous mapping. If $T_1$ is compact, then its image under $f$, $f[T_1] \subseteq T_2$, is also compact.

*Proof*: Suppose $V$ is an open cover of $f[T_1]$ by open sets in $T_2$ (i.e. $V$ is a potentially infinite set of open sets that cover $f[T_1]$). Since $f$ is continuous, we can use Theorem 1 from above to say that the preimage $f^{-1}[U]$ is open in $T_1$ for each open set $U \in V$. Therefore, $\curlybrackets{f^{-1}[U] ~\mid~U \in V}$ is an open cover of $T_1$. Since $T_1$ is compact, every cover has a finite subcover. Therefore, $\curlybrackets{f^{-1}[U_1], \dots, f^{-1}[U_r]}$ is an open cover of $T_1$ for $U_i \in V$ and a finite $r \in \bbN$. Then we know that

$$\bigcup_{i=1}^r f^{-1}[U_i] = T_1$$

by definition of open cover. But therefore $\bigcup_{i=1}^r U_i = T_2$. Thus, $\curlybrackets{U_1, \dots, U_r}$ is a finite open cover of $f[T_1]$. We chose $V$ arbitrarily, so we see that $f[T_1]$ admits a finite subcover for all open covers, and is therefore compact. {% include endproof.html %}



### Compactness on metric spaces

**Theorem 3**: Let $(X, d)$  be a metric space (e.g. a topological space with the open sets defined via the metric), and $K \subseteq X$ be compact. Then $K$ is closed and bounded.

*Proof*: We'll begin showing boundedness. Pick a $x \in K$. Let $U_n = B_n(x)$ be the open ball of radius $n$ around $x$ in $K$. Then $\curlybrackets{U_n~\mid~ n\in \bbN}$ is an open cover of $K$. Since $K$ is compact, it has a finite subcover. So $K \subseteq U_n$ for some finite $n$. Thus, $d(x, y) \leq 2n$ for all $x, y\in K$, meaning that $K$ is bounded. Now we'll show that $K$ is closed. Assume for the sake of contradiction that $K$ is not closed. Then $X\setminus K$ is not open, so $\exists x \in X\setminus K$ such that $\forall r>0$, $B_r(x) \not\subset X\setminus K$. Then $\exists y \in B_r(x)$ with $y \in K$. Therefore, for all $r>0$, 

$$B_r(x) \cap K \neq \emptyset. \qquad(*)$$

Now define for every $k \in K$, define $U_k = B_{d(x,k)/2}(k)$ and $V_k = B_{d(x, k)/2}(x)$. Notice that $U_k \cap V_k = \emptyset$, and $\curlybrackets{U_k~\mid~ k\in K}$ is an open cover of $K$. Since $K$ is compact, there exists a finite cover $\curlybrackets{U_{k_1}, \dots, U_{k_m}}$. So

$$U \coloneqq U_{k_1}\cup \dots \cup U_{k_m} \supseteq K$$

and

$$V \coloneqq V_{k_1}\cap \dots \cap V_{k_m}$$

is open since it is a finite intersection of open sets. Finally, we notice that $U \cap V = \emptyset$, so $V$ is an open neighborhood of $x$ that doesn't intersect $K$. But this contradicts $(*)$ from above. Therefore, our assumption that $K$ is not closed is incorrect. {% include endproof.html %}

I'd like to mention that this theorem does *not* work the other way; namely, closed and bounded does not necessarily imply compact. See [this example](https://math.stackexchange.com/a/323074/395731) for example.


<!-- PROVE THAT CLOSED AND BOUNDED IMPLIES COMPACT IN THIS CASE -->
<!-- #### Example of compactness on a metric space - the unitary group

Consider the unitary group $U(n)$ of $n \times n$ complex matrices. We can define a metric $d$ on $U(n)$ via the operator norm. For $U_1, U_2 \in U(n)$,

$$\begin{aligned}
d(U_1, U_2) &= \norm{U_1 - U_2}\\
&\coloneqq \sup\curlybrackets{\norm{(U_1-U_2)x}_2 ~\mid~ x \in \bbC^n, \norm{x}_2 = 1}.
\end{aligned}$$

Notice that $\norm U = 1$ for all $U \in U(n)$ since $U$ is an isometry. Therefore, for any $U_1, U_2 \in U(n)$,

$$\begin{aligned}
d(U_1, U_2) &= \norm{U_1 - U_2}\\
&\leq \norm{U_1} + \norm{U_2}\qquad \textrm{tri. ineq.}\\
&= 2.
\end{aligned}$$

This then proves that $U(n)$ is bounded. Now we consider the continuous function

$$\begin{aligned}
f:~ &\bbC^{n\times n} \to \bbC^{n\times n}\\
&A \mapsto A^\dag A.
\end{aligned}$$

Notice that $U(n) = f^{-1}[\curlybrackets I]$. $\curlybrackets I$ is closed. So Lemma 1 from above shows that $f^{-1}[\curlybrackets I]$ is closed since $f$ is continuous. Therefore, $U(n)$ is closed.

So we've shown that $U(n)$ is closed and bounded with respect to its metric topology. Thus, by Theorem 3 above, $U(n)$ is compact. {% include endproof.html %} -->


### Continuous functions from compact sets to $\bbR$

To prove Theorem 4, which is a useful application of compactness as a general property, we will first need the following lemma.

**Lemma 2**: Let $d$ be a metric so that $(\bbR, d)$ is a metric space. Suppose $A \subset \bbR$ is closed and bounded so that $\sup A$ and $\inf A$ exists. Then $\sup A \in A$ and $\inf A \in A$, meaning that $\sup A = \max A$ and $\inf A = \min A$.

*Proof*: We'll prove this for $\sup$; of course a similar proof holds for $\inf$. Define $s \coloneqq \sup A$. For the sake of contradiction, suppose $s \notin A$. Since $A$ is closed, $\bbR \setminus A$ is open. Therefore, $\exists r > 0$ such that $B_r(s) \cap A = \emptyset$. Then $B_r(x)$ contains upper bounds on $\sup A$ that are lower than $s$. This implies that $s \neq \sup A$, which contradicts our assumption. {% include endproof.html %}

**Theorem 4**: Let $X$ be a topological space with some topology. Let $K \subseteq X$ be a compact set. Let $d$ be a metric so that $(\bbR, d)$ is a metric space. Then any continuous function $f: K \to \bbR$ attains a minimum and maximum value on $K$.

*Proof*: Since $f$ is continuous and $K$ is compact, we can use Theorem 2 to say that the image $f[K]$ is compact. Since $\parentheses{\bbR, d}$ is a metric space, we know from Theorem 3 that $f[K]$ being compact implies that it is closed and bounded with respect to the metric $d$. Since $f[K]$ is bounded, it has a supremum and infimum. Since it is closed, then Lemma 2 above tells us that it contains its supremum and infimum. Therefore, $f[K]$ has a maximum and minimum. {% include endproof.html %}

Note here that this works for any topological space $X$ and any compact set $K \subseteq X$; $X$ need not be a metric space. I feel as though Theorem 4 is one of the first actual applications of general compactness one encounters. Prior to this, most applications have been with respect to metric spaces, where we could have never defined compactness and instead just always said "closed and bounded". But this theorem works for general topological spaces, and so is perhaps a reason to care about compactness as a topological property.


#### References

- [Applied Analysis, Hunter and Nachtergaele](https://www.google.com/books/edition/Applied_Analysis/oOYQVeHmNk4C?hl=en)
- [https://www.reddit.com/r/math/comments/lbldwt/compactness/glvm6ld/?context=3](https://www.reddit.com/r/math/comments/lbldwt/compactness/glvm6ld/?context=3)
- [https://proofwiki.org/wiki/Continuous_Image_of_Compact_Space_is_Compact](https://proofwiki.org/wiki/Continuous_Image_of_Compact_Space_is_Compact)
- [https://math.stackexchange.com/questions/109548/x-compact-metric-space-fx-rightarrow-mathbbr-continuous-attains-max-min?rq=1](https://math.stackexchange.com/questions/109548/x-compact-metric-space-fx-rightarrow-mathbbr-continuous-attains-max-min?rq=1)
- [https://math.stackexchange.com/questions/1723289/show-that-the-special-unitary-group-sun-is-a-compact-topological-group](https://math.stackexchange.com/questions/1723289/show-that-the-special-unitary-group-sun-is-a-compact-topological-group)
- [https://math.stackexchange.com/questions/671999/on-proving-that-a-compact-metric-space-is-bounded](https://math.stackexchange.com/questions/671999/on-proving-that-a-compact-metric-space-is-bounded)
- [https://math.stackexchange.com/questions/2111662/prove-compact-subsets-of-metric-spaces-are-closed](https://math.stackexchange.com/questions/2111662/prove-compact-subsets-of-metric-spaces-are-closed)
- [https://math.stackexchange.com/questions/75608/does-a-closed-and-bounded-set-in-mathbbr-necessarily-contain-its-supremum-a](https://math.stackexchange.com/questions/75608/does-a-closed-and-bounded-set-in-mathbbr-necessarily-contain-its-supremum-a)
- [https://math.stackexchange.com/questions/437829/the-preimage-of-continuous-function-on-a-closed-set-is-closed](https://math.stackexchange.com/questions/437829/the-preimage-of-continuous-function-on-a-closed-set-is-closed)
- [https://math.stackexchange.com/a/109552/395731](https://math.stackexchange.com/a/109552/395731)
- [https://math.stackexchange.com/a/1723302/395731](https://math.stackexchange.com/a/1723302/395731)


{% include post-footer.html %}
