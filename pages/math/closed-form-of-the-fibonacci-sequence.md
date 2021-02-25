---
title: Closed form of the Fibonacci sequence
comments: 13
---

{% include post-header.md %}

(25 Feb 2021) This is a pretty standard exercise in linear algebra to get a feeling for how to use eigenvalues and eigenvectors. Let's go through it here. 

**Definition**: The *Fibonacci sequence* is the sequence $$(F_n)_{n \in \NN}$$ satisfying
1. $$F_1 = F_2 = 1$$ (for convenience below, we'll define $$F_0 = 0$$ here), and
2. $$\forall n \geq 2: F_{n+1} = F_{n-1} + F_{n}.$$

Thus, the Fibonacci sequence is 

$$1, 1, 2, 3, 5, 8, 13, 21, \dots.$$

Let's define the following

$$\mathcal F_n \coloneqq \parentheses{\begin{matrix}F_n, F_{n-1} \end{matrix}}.$$

Using

$$\parentheses{\begin{matrix}F_{n+1}, F_{n} \end{matrix}} = \parentheses{\begin{matrix}F_n + F_{n-1}, F_n \end{matrix}},$$

we see that $$\mathcal F_{n+1} = M \mathcal F_n$$ where

$$M = \parentheses{\begin{marix}1&1\\1&0 \end{matrix}}.$$

Then we use that $$\mathcal F_1 = (1, 0)^T$$ (i.e. $$F_1 = 1, F_0 = 0$$) to find

$$\mathcal F_{n+1} = M^n \mathcal F_1.$$

If you work through the exercise, you will find that $$M$$ has the two pairs of (eigenvalues, eigenvectors) $$(\lambda_i, v_i)$$ with

$$\begin{aligned}
\lambda_1 &= \frac{1+\sqrt 5}{2}\\
\lambda_2 &= \frac{1-\sqrt 5}{2}\\
v_1 &= \parentheses{\begin{matrix}\lambda_1\\1 \end{matrix}}\\
v_2 &= \parentheses{\begin{matrix}\lambda_2\\1 \end{matrix}}.
\end{aligned}$$

Recall these are found by requiring that $$M v_i = \lambda_i v_i$$ per the definition of eigenvalues and eigenvectors, which becomes a simple algebraic exercise. We write

$$\mathcal F_1 = a v_1 + b v_2.$$

We know we can do this because the set $$\braces{v_1, v_2}$$ is a basis for $$\RR^2$$. It is then straightforward to verify that 

$$a = \frac{1}{\lambda_1-\lambda_2} = \frac{1}{\sqrt{5}}$$

and $$b = -a$$. Using the definition of eigenvectors and eigenvalues, we can then show that

$$\begin{aligned}
\parentheses{F_{n+1}\\F_n} &= \mathcal F_{n+1}\\
&= M^n \mathcal F_1\\
&= aM^n v_1 + b M^n v_2\\
&= a \lambda_1^n v_1 + b \lambda_2^n v_2\\
&= \parentheses{\begin{matrix}a \lambda_1^{n+1} + b \lambda_2^{n+1} \\ a\lambda_1^n + b \lambda_2^n \end{matrix}}.
\end{aligned}$$

So we arrive at a closed form for the Fibonacci number $$F_n$$, namely

$$F_n = a\lambda_1^n + b \lambda_2^n.$$

Using our values for $$a, b, \lambda_1,$$ and $$\lambda_2$$ above, we find the closed form for the Fibonacci numbers to be

$$F_n = \frac{1}{\sqrt{5}}\parentheses{\parentheses{\frac{1+\sqrt 5}{2}}^n - \parentheses{\frac{1-\sqrt 5}{2}}^n}.$$


#### Golden Ratio

I will note here that we see explictly in the formula that the Golden Ratio is involved! Namely, $$\lambda_1$$ and $$\lambda_2$$ are the Golden Ratios. Check out [this video](https://www.youtube.com/watch?v=sj8Sg8qnjOg) for some more on the Golden Ratio. But I will briefly discuss it here. The Golden Ratio is defined as the ratio $$x / y$$ that satisfies 

$$\frac{x+y}{x} = \frac{x}{y}.$$

It then should be no surpise that the Golden Ratio shows up in the Fibonacci sequence; suppose $$x = F_{n}$$ and $$y = F_{n-1}$$. Then, using $$F_{n+1} = F_n + F_{n-1}$$,

$$\begin{aligned}
\frac{x+y}{x} &= \frac{F_n + F_{n-1}}{F_n}\\
&= \frac{F_n + F_{n-1}}{F_{n-1} + F_{n-2}}\\
&\substack{=\\n\to\infty} \frac{F_n}{F_{n-1}}\\
&= \frac{x}{y},
\end{aligned}$$


{% include post-footer.html %}
