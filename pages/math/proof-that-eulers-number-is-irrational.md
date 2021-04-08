---
title: Proof that Euler's number is irrational
comments: 7
---

{% include post-header.md %}

(25 Jan 2021) Reiterating perhaps the main point of my website, I hope to organize the many small things that I learn as I go along so that they are easily accessible for future reference. With that in mind, this post will follow this [great video by Numberphile](https://youtu.be/xOXsDfMMTjs) that proves the irrationality of Euler's number $e$. The video itself is over sixteen minutes long, but this post should be much more quickly readable.

Let's first review a very simple proof that $\sqrt{2}$ is irrational.

**Theorem**: $\sqrt{2}$ is irrational.

*Proof*: Proof by contradiction. First, assume that $\sqrt{2} = a/b$ is rational so that $a$ and $b$ are coprime natural numbers. Then $2 = a^2/b^2$, meaning that $a^2$ is even. It is simple to check then that $a$ must itself be even. So we can write $a = 2z$ for some number $z$. Therefore, $2 = (2z)^2 / b^2$, giving that $b^2 = 2z^2$. Thus, $b^2$ is also even, and as result $b$ is even. $a$ and $b$ were assumed to be coprime, but we've just deduced that they are both even (and therefore not coprime). We've reached a contradiction, meaning that $\sqrt 2$ must not be rational. {% include endproof.html %}

For the main theorem, we will need the following lemma.

**Lemma**: For any $x \in [0, 1)$,

$$\sum_{n=1}^\infty x^n = \frac{x}{1-x}.$$

*Proof*: Let $S \coloneqq x+x^2+x^3+\dots$. Then $S/x - S = 1.$ So $S = 1/(1/x-1)$, completing the proof. {% include endproof.html %}

**Theorem**: $e$ is irrational.

*Proof*: Proof by contradiction. First, assume that $e = a/b$ is rational so that $a$ and $b$ are coprime. We know that

$$e = 1+\frac{1}{1!} + \frac{1}{2!} + \frac{1}{3!} + \dots$$

by a Taylor expansion of $e^x$. So

$$a / b = 1+\frac{1}{1!} + \frac{1}{2!} + \frac{1}{3!} + \dots$$

Then

$$\begin{aligned}
\bbZ \ni (b!)\frac{a}{b} =& \underbrace{b! + \frac{b!}{1!} + \dots + \frac{b!}{b!}}_{\eqqcolon C\in \bbZ}\\
&~~+ \underbrace{\frac{1}{b+1} + \frac{1}{(b+1)(b+2)} + \frac{1}{(b+1)(b+2)(b+3)} + \dots}_{\eqqcolon D}.
\end{aligned}$$

The left-hand side is an integer, and so is $C$. Therefore, $D$ must also be an integer. Now we will bound the value of $D$. Clearly, $D > 0$ since it is a sum of strictly positive terms. Now let's upper bound it.

$$\begin{aligned}
D &= \frac{1}{b+1} + \frac{1}{(b+1)(b+2)} + \dots\\
&< \frac{1}{b+1} + \frac{1}{(b+1)^2} + \frac{1}{(b+1)^3}+ \dots\\
&= \sum_{n=1}^{\infty} \parentheses{\frac{1}{b+1}}^n\\
&= \frac{1/(b+1)}{1-1/(b+1)},
\end{aligned}$$

where we used the Lemma in the last line. In summary, we've shown that $0 < D < 1/b.$ But recall our assumption that $e$ was rational immediately implied that $D$ was an integer. The bounds we found contradict this assumption, since they imply that $0 < D < 1$. We've reached a contradiction, meaning that $e$ must not be rational. {% include endproof.html %}


{% include post-footer.html %}
