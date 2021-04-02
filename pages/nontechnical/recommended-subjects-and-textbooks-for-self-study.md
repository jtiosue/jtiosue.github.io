---
title: Recommended subjects and textbooks for self-study (for physicists)
comments: 12
---

{% include post-header.md %}

(27 Feb 2021) When I started my undergraduate at MIT, I was pretty sure I wanted to major in physics, but I couldn't decide whether or not to double major in math. I talked to upperclassmen, and they almost all said that double majoring is a bad idea because I would not have enough time to take all the cool classes in either of the majors. They said that I would only be able to scratch the surface of each subject, rather than going deep into one or the other. So I decided to just stick with a single major in physics. This is my biggest regret of all my decisions in undergrad.

I took more classes than most every semester, and I did very well in all of them. I did all of the homeworks, and even most of the extra readings that professors would suggest. Yet, I came out of undergrad not knowing anything about group theory or representation theory. I'm finding out more and more that a *huge* portion of physics is just representations of interesting symmetry groups! One of the most beautiful things I've ever learned is that fundamental particles are irreducible representations of the Poincaré group. I learned nothing of topological spaces, for example, which are the basis for pretty much everything. I went through so many quantum courses never learning about the many ways functional analysis is different from linear algebra; we work in these infinite-dimensional vector spaces all the time, but the complications of this were never addressed (e.g. $$\Tr[A, B] = 0$$ by the cyclic invariance of the trace, but $$\Tr \brackets{\hat x, \hat p} = i\hbar \dim \mathcal H$$ for the Hilbert space $$\mathcal H$$). I never learned anything about measures or the Lebesgue measure. Now, in graduate school, the Haar measure is becoming of interest in my research, so of course I've had to work through learning measure theory as best as I can.

I am now of the strong belief that math classes are potentially more important to a theoretical physicist than physics classes. I personally feel as though I have learned much more about *physics* through my self-study of various *math* topics.


## Subjects and textbooks

Some of these are subjects I *wish* I knew (or I wish I knew better), and some of these are those that I feel as though I learned well through the resources mentioned.


#### Linear algebra

I used [Linear Algebra Done Right, by Sheldon Axler](https://linear.axler.net/) in my early years of undergrad. It is a wonderful book as an introduction to linear algebra, and it really is essential that every physicist have a solid understanding of linear algebra. I completely agree with his viewpoint on determinants (see [Down with Determinants](https://www.axler.net/DwD.html)). They seem to often take away from the essence of what linear algebra is, especially when speaking in an abstract sense. That being said, the determinant is used often and it is useful in practice. I felt as though I didn't have a very good understanding of determinants for a while, probably because they were neglected in this book moreso than in others (though he does cover them briefly in the end). But I think it is 100% worth it, because I've always felt that I have a great understanding of linear algebra as a whole. The stuff I learned [here](../math/levi-civita-determinants-volumes-and-jacobians.md) really cleared up determinants for me.


#### Tensors

Tensors were always very cryptic to me. I learned them very briefly in my relativity class, where we quickly passed through the details and instead just focused on how to use them. The standard description that a tensor *transforms* in a certain way never did it for me. The first part of [An Introduction to Tensors and Group Theory for Physicists, by Nadir Jeevanjee](https://www.amazon.com/Introduction-Tensors-Group-Theory-Physicists/dp/3319147935) is all on tensors, and it really helped me grasp tensors, and relativity, a lot better. He introduces tensors and they should be introduced, as multilinear maps, and then from that shows how everything else falls out, including the transformation properties. From this textbook, I got a much better understanding of what the metric (e.g. Minkowski metric) in relativity really is.


#### Group theory and representation theory

Group theory is one of the most beautiful subjects I've ever encountered. It is so beautiful how it connects so much of physics in such an elegant way. I also firmly believe that a physicst should learn group theory, specifically Lie group theory, as soon as they can, because it seems to apply to everything. I used the second part of [An Introduction to Tensors and Group Theory for Physicists, by Nadir Jeevanjee](https://www.amazon.com/Introduction-Tensors-Group-Theory-Physicists/dp/3319147935) to learn group theory. I think it's good, but I don't have anything else to compare it to. To get a full understanding of Lie groups, one needs differntial geometry, which this textbook does not do. It is a nice and quick way to get up to speed on group theory and I would definitely recommend it. I look forward to reading other textbooks to get a more sophisticated view Lie groups and their applications.

I just started [these lectures](https://www.youtube.com/playlist?list=PL8yHsr3EFj53RWBkiHKoOsTw-dGHAoJ-h) by Richard Borcherds. They are awesome. He has a bunch of amazing lectures on YouTube.


#### Differential geometry

I have not yet learned differential geometry, though I am now sitting in on lectures. I would definitely recommend this be one of the subjects physicists learn, since it has applications everywhere, including relativity and group theory.


#### Functional analysis and measure theory

These are two subject I believe are essential to theoretical physicists, although they seem to always be neglected. I have read through some of [Applied Analysis, by Hunter and Nachtergaele](https://www.amazon.com/Applied-Analysis-John-K-Hunter/dp/9812705430) which has been great and I plan to finish. I've also been watching through these [functional analysis lectures](https://www.youtube.com/playlist?list=PLBh2i93oe2qsGKDOsuVVw-OCAfprrnGfr) and these [measure theory lectures](https://www.youtube.com/playlist?list=PLBh2i93oe2qvMVqAzsX1Kuv6-4fjazZ8j). I think they started out great, but in the later videos I think he needs to give more proofs or proof sketches as opposed to just stating theorems and moving on. I also think they could be a lot better with some examples from physics.


#### Classical complexity theory

I've loved this book so far: [Computational Complexity: A Modern Approach, by Arora and Barak](http://theory.cs.princeton.edu/complexity/).


#### Complex analysis

[Great lectures](https://www.youtube.com/playlist?list=PL8yHsr3EFj537_iYA5QrvwhvMlpkJ1yGN) by Richard Borcherds.


#### Miscellaneous

[These lectures](https://www.youtube.com/playlist?list=PLBh2i93oe2qtbygdXz4u6Mkh7c_hMLBA8) have been really fun to quickly learn some basic fundamental math things I'd never known.


{% include post-footer.html %}
