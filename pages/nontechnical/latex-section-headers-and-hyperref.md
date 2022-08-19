---
title: LaTeX section headers and hyperref
comments: 31
---

{% include post-header.md %}

(19 Aug 2022) Suppose you have a theorem labeled `thm:1`, and that you want to labeled a section as `\section{Proof of \cref{thm:1}}`, where `\cref` comes from the cleveref package. If you're using hyperref, this will cause a warning "Package hyperref Warning: Token not allowed in a PDF string". Everything on the pdf will look great, and there will be a hyperlink in the section header that takes you to the theorem. But if you look at the table of contents or outline of the pdf document as shown in a pdf viewer, you will see the section referenced as "Proof of thm:1". The workaround is as follows:

{% raw %}

```latex
\section{Proof of \texorpdfstring{\cref{thm:1}}{\autoref*{thm:1}}}
```

{% endraw %}

Notably, `\cref*` and `\autoref*` get rid of the link, and so on the pdf outline it will properly show the theorem number. On the other hand, in the actual pdf, `\cref` is still being used; that's what `texorpdfstring` does. Weirdly, though, using `\cref*` for the pdf string doesn't get rid of the warning, so instead we use `\autoref*` here.

The same principle works for section headers with math. Namely, instead of 

{% raw %}

```latex
\section{Proof that $1+1=2$}
```

{% endraw %}

do

{% raw %}

```latex
\section{Proof that \texorpdfstring{$1+1=2$}{1+1=2}}
```

{% endraw %}


#### References

- [https://tex.stackexchange.com/questions/53513/hyperref-token-not-allowed](https://tex.stackexchange.com/questions/53513/hyperref-token-not-allowed)
- [https://tex.stackexchange.com/questions/6093/selectively-turn-off-hyperref-links](https://tex.stackexchange.com/questions/6093/selectively-turn-off-hyperref-links)


{% include post-footer.html %}
