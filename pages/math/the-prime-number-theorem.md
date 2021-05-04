---
title: The Prime Number Theorem
comments: 3
---

{% include post-header.md %}

(17 Jan 2021) For my own education, I followed [Michael Nielsen](https://twitter.com/michael_nielsen/status/1342181807630897157?s=19)'s post on the subject and wrote in the details. As he mentions, this is not the most common (I don't think) proof of the Prime Number Theorem, but it is a cool and easy one. The Prime Number Theorem states that the number of prime numbers $\leq n$ is $\Theta(n/\ln n)$. As far as I know, the proof we show here only shows that it is $\Omega(n/\ln n)$, and so it remains to be shown that it is also $\mathcal O(n/\ln n)$. Let's begin.

**Definitions**: 
- $\mathbb P \coloneqq \curlybrackets{p \in \mathbb N ~\mid~ p \textrm{ is prime} }$ is the set of of all prime numbers.
- $\pi(n) \coloneqq \left\lvert \mathbb P \setminus [n+1, \infty)  \right\rvert$ is the number of prime numbers less than or equal to $n$.
- $P_p: \mathbb N \to \mathbb N_0$ for $p \in \mathbb P$ is defined such that $P_p(x)$ is the prime power of $p$ in the prime factorization of $x$. Thus for any $x \in \mathbb N$, we have that $x = \prod_{p\in \mathbb P} p^{P_p(x)}$.

**Lemma 1**: $\forall n\in \mathbb N:~{2n \choose n} \geq 2^n$.

*Proof*: We'll prove by induction on $n$. For the base case, $n=1$, we have that ${2 \choose 1} = 2 \geq 2^1$. Next, we assume that the lemma is true for $n$, and show that implies that the lemma is true for $n+1$. In the following, we use the induction hypothesis to go from the first line to the second line.

$$\begin{aligned} {2(n+1) \choose n+1} &= \frac{(2n+2)(2n+1)}{(n+1)^2}{2n \choose n} \\
&\geq \frac{(2n+2)(2n+1)}{(n+1)^2}2^n\\
&= \frac{2n+1}{n+1} 2^{n+1}\\ &\geq 2^{n+1}.
\end{aligned}$$

So we have proved the lemma. {% include endproof.html %}


**Lemma 2**: $\forall p\in \mathbb P: P_p\left({2n \choose n} \right) \leq \log_p 2n$.

*Proof*: First notice some simple properties of $P_p$; namely that for any $a, b \in \mathbb N$, we have that $P_p(ab) = P_p(a) + P_p(b)$. Similarly, if $a/b \in \mathbb N$, then $P_p(a/b) = P_p(a) - P_p(b)$.

Let's first consider the $p=2$ case.

$$\begin{aligned}
P_2(n!) &= P_2(1) + P_2(2) + P_2(3) + \dots + P_2(n)\\
&= P_2(2) + P_2(4) + P_2(6) + \dots \quad \textrm{since } P_2(\textrm{odd number}) = 0\\
&= P_2(2\cdot 1) + P_2(2\cdot 2) + P_2(2\cdot 3) + \dots\\
&= (P_2(2) + P_2(1)) + (P_2(2) + P_2(2)) + (P_2(2) + P_2(3)) + \dots\\
&= \lfloor n/2 \rfloor \cdot P_2(2) + P_2(1) + P_2(2) + P_2(3) + \dots\\
&= \lfloor n/2 \rfloor + P_2(\lfloor n/2 \rfloor!).
\end{aligned}$$

Similarly, for general $p \in \mathbb P$: $P_p(n!) = \lfloor n/p\rfloor + P_p(\lfloor n/p \rfloor!)$. So,

$$\begin{aligned}
P_p(n!) &= \lfloor n/p\rfloor + P_p(\lfloor n/p \rfloor!)\\
&= \lfloor n/p\rfloor + \lfloor n/p^2\rfloor + P_p(\lfloor n/p^2 \rfloor!)\\
&= \dots\\
&= \sum_{i=1}^\infty \lfloor n/p^i\rfloor\\
&= \sum_{i=1}^{\lfloor \log_p n \rfloor} \lfloor n/p^i\rfloor.
\end{aligned}$$

Then,

$$\begin{aligned}
P_p\left({2n \choose n} \right) &= P_p((2n)!) - 2P_p(n!)\\
&= \sum_{i=1}^{\lfloor \log_p 2n \rfloor} \lfloor 2n/p^i\rfloor - 2\sum_{i=1}^{\lfloor \log_p n \rfloor} \lfloor n/p^i\rfloor\\
&= \sum_{i=1}^{\lfloor \log_p 2n \rfloor} \left(\lfloor 2n/p^i \rfloor - 2\lfloor n/p^i\rfloor \right)\\
&\leq \sum_{i=1}^{\lfloor \log_p 2n \rfloor} (1)\\
&= \lfloor \log_p 2n \rfloor\\
&\leq \log_p 2n
\end{aligned}$$

as desired. {% include endproof.html %}


Finally, we get to the main theorem.

**Theorem**: $\pi(n) \in \Omega(n / \ln n)$.

*Proof*: How can we build up a very large number from a product of small primes to small powers (i.e. lemma 2 implies small powers)? Answer: must have a lot of distinct primes!

$$\begin{aligned}
2^n &\leq {2n \choose n} \quad \textrm{by lemma 1}\\
&= \prod_{p\in \mathbb P} p^{P_p\left({2n \choose n} \right)} \quad \textrm{by definition of } P_p\\
&\leq \prod_{p \in \mathbb P\setminus[2n+1, \infty)}p^{\log_p 2n} \quad \textrm{by lemma 2}\\
&= (2n)^{\pi(2n)} \quad \textrm{by definition of }\pi.
\end{aligned}$$

Taking the $\ln$ of both sides and rearranging then gives $\pi(n) \geq \frac{n\ln 2}{4\ln n + 4\ln 2} \in \Omega(n / \ln n)$ as desired. {% include endproof.html %}
 

As mentioned before, one can also prove (although I don't think you can do it with the same method as above) that $\pi(n) \in \mathcal O(n / \ln n)$. Then we get that $\pi(n) \in \Theta(n/\ln n)$, which is the Prime Number Theorem.


**Corollary**: for large $n$, the probability that a random integer $\leq n$ is prime is close to $1/\ln n$.


{% include post-footer.html %}
