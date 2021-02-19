---
title: Why Newton's law of gravitation?
comments: 1
---

{% include post-header.md %}

(15 Jan 2021) We postulate the magnitude of the gravitational force between two masses to be a function $$F(m_1, m_2, \vec r_1, \vec r_2)$$. Due to the translational invariance of space, $$F$$ should not depend on the absolute location in space, but rather the relative location of the two masses; e.g. 

$$F(m_1, m_2, \vec r_1 + \vec a, \vec r_2 + \vec a) = F(m_1, m_2, \vec r_1, \vec r_2).$$

Therefore, the force is $$F(m_1, m_2, \vec r_1 - \vec r_2)$$. Since we assume that there is no special direction in space,

$$F(m_1, m_2, R(\vec r_1 - \vec r_2)) = F(m_1, m_2, \vec r_1 - \vec r_2)$$

for any rotation $$R \in$$ SO$$(3)$$. Therefore, the force is $$F(m_1, m_2, \norm{\vec r_1 - \vec r_2})$$. Let's define $$r \coloneqq \norm{\vec r_1 - \vec r_2}$$, so $$F(m_1, m_2, r)$$.

Next we make the assumption that mass and space are decoupled; that is, we expect the force between two masses to decay at the same rate with distance regardless of the values of the mass. Therefore $$F(m_1, m_2, r) = f(m_1, m_2) g(r)$$. If we consider the gravitational force to be like a field, we've already determined that the field is spherically symmetric (a function of $$r$$ only). Then the density of the field lines at a fixed radius $$r$$ will decay with the surface area of the sphere. Thus we expect $$g(r) \propto 1/r^2$$. Let's call the proportionality constant $$G$$. Then we have $$F(m_1, m_2, r) = G f(m_1, m_2) / r^2$$.

Now let's figure out $$f(m_1, m_2)$$. We consider the Earth - Sun system as an example. The Earth with mass $$M_e$$ has a mass that is equal to the sum of its parts, and indeed there are many parts. Many tiny rocks, big boulders, etc. contribute to $$M_e$$. But we expect that this should not affect the force. In other words, $$f(\sum_i m_i, m) = \sum_i f(m_i, m)$$ and $$f(m, \sum_i m_i) = \sum_i f(m, m_i)$$. This then means that $$f(m_1, m_2)$$ is a bilinear map. The only choice then is $$f(m_1, m_2) \propto m_1 m_2$$. We can absorb any proportionality constant into $$G$$.

Thus, we get our final result $$F = G m_1 m_2 / r^2$$.

Of course many of our assumptions are incorrect, and that's why we eventually go to General Relativity.


{% include post-footer.html %}

