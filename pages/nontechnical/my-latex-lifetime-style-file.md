---
title: My LaTeX lifetime style file
comments: 14
---

{% include post-header.md %}

(Updated 31 Oct 2022) Over the years, I've learned that LaTeX is really quite wonderful. Many have suggested that I have a "lifetime style file" that I add to my LaTeX documents with `\usepackage{lifetime.sty}`. So I created one, and will (probably) continue updating it as I go along. By the way, one of the things I most wish I knew about LaTeX a long time ago was the ability to separate documents into multiple files and compile them into one file via the `\input{}` command. Or, even better, is the `\import{path}{file}` command, which updates the path in the import so you can use relative paths in your document.

{% raw %}

```latex
% \usepackage[left=1in,right=1in,top=1in,bottom=1in]{geometry}
\usepackage{amsmath,amssymb,amsthm,amsfonts,bm,graphicx,mathtools,import,ifthen,xcolor}
\allowdisplaybreaks

% to allow for defining commands with *
% e.g. see \note and \note* below
\usepackage{suffix}

% newline for new paragraph
% \usepackage[parfill]{parskip}

% ONLY FOR DRAFTING, COMMENT THIS OUT FOR THE FINAL DOCUMENT.
\usepackage{showkeys}

% for dummy words, use with \lipsum or \lipsum[50], etc.
\usepackage{lipsum}

% Make theorems in appendix labeled by section
\usepackage{apptools}
\AtAppendix{\counterwithin{theorem}{section}}

% Make figures in appendix labeled by section
\let\oldappendix\appendix
\renewcommand\appendix{\oldappendix
    % footnotes are different with revtex
    % \setcounter{footnote}{0} 
    % counters should reset each section
    \counterwithin{figure}{section}
    \counterwithin{table}{section}
    % footnote formatting
    % \renewcommand*{\thefootnote}{\fnsymbol{\fontsize{10pt}{10pt}footnote}}
}

% meta
\newcommand{\iosuename}{Joseph~T.~Iosue}
\newcommand{\iosueemail}{\href{mailto:jtiosue@umd.edu}{jtiosue@umd.edu}}
\newcommand{\UMD}{University~of~Maryland,~College~Park,~Maryland~20742,~USA}
\newcommand{\JQI}{Joint~Quantum~Institute, NIST/\UMD}
\newcommand{\QUICS}{Joint~Center~for~Quantum~Information~and~Computer~Science, NIST/\UMD}

% to label equations by section, e.g. equation 1.3, 2.5, etc.
% \numberwithin{equation}{section}

% for ``commenting out'' chunks of text 
\newcommand{\ignore}[1]{}
% for notes on the text 
\newcommand{\note}[1]{{\color{red} [#1]}}
\WithSuffix\newcommand\note*[1]{{\color{red} #1}}

% supposed to be loaded last
% lintocpage makes the page numbers be linked in the 
% table of contents instead of the section titles.
\usepackage[colorlinks,citecolor=blue,bookmarks=true,breaklinks=true,linktocpage=true]{hyperref}
% make ref to figure go to top of figure instead of to caption
\usepackage[all]{hypcap}

% Makes ligatured fonts searchable and copyable in pdf readers. Should be loaded after hyperref
\usepackage{cmap}

% for stuff like ï. Should be after cmap
\usepackage[T1]{fontenc}

% needs to be loaded after hyperref
\usepackage[capitalize]{cleveref}

% headings after \notoc will not be in the table of contents
% headings after \toc will be
\let\originaladdtocontents\addtocontents
\newcommand{\notoc}{\renewcommand{\addtocontents}[2]{}}
\newcommand{\toc}{\let\addtocontents\originaladdtocontents}

% theorems and etc.
\newtheorem{theorem}{Theorem}%[section]
\newtheorem{claim}[theorem]{Claim}
\newtheorem{proposition}[theorem]{Proposition}
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem{corollary}[theorem]{Corollary}
\newtheorem{conjecture}[theorem]{Conjecture}
\newtheorem{fact}[theorem]{Fact}
\newtheorem{definition}[theorem]{Definition}
\theoremstyle{remark}\newtheorem{remark}[theorem]{Remark}
\theoremstyle{remark}\newtheorem{observation}[theorem]{Observation}
% \theoremstyle{definition}\newtheorem{example}[theorem]{Example}
\theoremstyle{definition}\newtheorem{examplex}[theorem]{Example}
\newenvironment{example}
  {\pushQED{\qed}\renewcommand{\qedsymbol}{$\diamond$}\examplex}
  {\popQED\endexamplex}
  
% number aligned equations as subequations. uses ifthen
% usage: just like align. But if you want to label the full block, include optional arg \begin{salign}[eq:label]
\newenvironment{salign}[1][]{
    \subequations
    \ifthenelse{\equal{#1}{}}
        {}
        {\label{#1}}
    \align
}{
    \endalign\endsubequations
}

% bb
\newcommand{\bbA}{\mathbb{A}}
\newcommand{\bbB}{\mathbb{B}}
\newcommand{\bbC}{\mathbb{C}}
\newcommand{\bbD}{\mathbb{D}}
\newcommand{\bbE}{\mathbb{E}}
\newcommand{\bbF}{\mathbb{F}}
\newcommand{\bbG}{\mathbb{G}}
\newcommand{\bbH}{\mathbb{H}}
\newcommand{\bbI}{\mathbb{I}}
\newcommand{\bbJ}{\mathbb{J}}
\newcommand{\bbK}{\mathbb{K}}
\newcommand{\bbL}{\mathbb{L}}
\newcommand{\bbM}{\mathbb{M}}
\newcommand{\bbN}{\mathbb{N}}
\newcommand{\bbO}{\mathbb{O}}
\newcommand{\bbP}{\mathbb{P}}
\newcommand{\bbQ}{\mathbb{Q}}
\newcommand{\bbR}{\mathbb{R}}
\newcommand{\bbS}{\mathbb{S}}
\newcommand{\bbT}{\mathbb{T}}
\newcommand{\bbU}{\mathbb{U}}
\newcommand{\bbV}{\mathbb{V}}
\newcommand{\bbW}{\mathbb{W}}
\newcommand{\bbX}{\mathbb{X}}
\newcommand{\bbY}{\mathbb{Y}}
\newcommand{\bbZ}{\mathbb{Z}}

% cal
\newcommand{\calA}{\mathcal{A}}
\newcommand{\calB}{\mathcal{B}}
\newcommand{\calC}{\mathcal{C}}
\newcommand{\calD}{\mathcal{D}}
\newcommand{\calE}{\mathcal{E}}
\newcommand{\calF}{\mathcal{F}}
\newcommand{\calG}{\mathcal{G}}
\newcommand{\calH}{\mathcal{H}}
\newcommand{\calI}{\mathcal{I}}
\newcommand{\calJ}{\mathcal{J}}
\newcommand{\calK}{\mathcal{K}}
\newcommand{\calL}{\mathcal{L}}
\newcommand{\calM}{\mathcal{M}}
\newcommand{\calN}{\mathcal{N}}
\newcommand{\calO}{\mathcal{O}}
\newcommand{\calP}{\mathcal{P}}
\newcommand{\calQ}{\mathcal{Q}}
\newcommand{\calR}{\mathcal{R}}
\newcommand{\calS}{\mathcal{S}}
\newcommand{\calT}{\mathcal{T}}
\newcommand{\calU}{\mathcal{U}}
\newcommand{\calV}{\mathcal{V}}
\newcommand{\calW}{\mathcal{W}}
\newcommand{\calX}{\mathcal{X}}
\newcommand{\calY}{\mathcal{Y}}
\newcommand{\calZ}{\mathcal{Z}}

% brackets
\newcommand{\parentheses}[1]{\left(#1\right)}
\newcommand{\brackets}[1]{\left[#1\right]}
\newcommand{\curlybrackets}[1]{\left\{#1\right\}}
\newcommand{\set}{\curlybrackets}
\newcommand{\pargs}[1]{\!\parentheses{#1}}
\newcommand{\bargs}[1]{\!\brackets{#1}}
\newcommand{\cbargs}[1]{\!\curlybrackets{#1}}
\newcommand{\angles}[1]{\left\langle #1\right\rangle}
\newcommand{\ceil}[1]{\left\lceil #1\right\rceil}
\newcommand{\floor}[1]{\left\lfloor #1\right\rfloor}
\newcommand{\abs}[1]{\left\lvert #1 \right\rvert}
\newcommand{\norm}[1]{\left\lVert #1 \right\rVert}
% with *, don't automatically size
\WithSuffix\newcommand\parentheses*[1]{(#1)}
\WithSuffix\newcommand\brackets*[1]{[#1]}
\WithSuffix\newcommand\curlybrackets*[1]{\{#1\}}
\WithSuffix\newcommand\pargs*[1]{(#1)}
\WithSuffix\newcommand\bargs*[1]{[#1]}
\WithSuffix\newcommand\cbargs*[1]{\{#1\}}
\WithSuffix\newcommand\angles*[1]{\langle #1\rangle}
\WithSuffix\newcommand\ceil*[1]{\lceil #1\rceil}
\WithSuffix\newcommand\floor*[1]{\lfloor #1\rfloor}
\WithSuffix\newcommand\abs*[1]{\lvert #1 \rvert}
\WithSuffix\newcommand\norm*[1]{\lVert #1 \rVert}

% brakets
\makeatletter
\newcommand{\ket}[1]{\@ifnextchar\bra{\mathinner{\lvert#1\rangle}\!}{\mathinner{\lvert#1\rangle}}}
\newcommand{\bra}[1]{\@ifnextchar\ket{\mathinner{\langle#1}\!}{\mathinner{\langle#1\rvert}}}
\newcommand{\Ket}[1]{\@ifnextchar\Bra{\mathinner{\big\lvert#1\big\rangle}\!}{\mathinner{\big\lvert#1\big\rangle}}}
\newcommand{\Bra}[1]{\@ifnextchar\Ket{\mathinner{\big\langle#1}\!}{\mathinner{\big\langle#1\big\rvert}}}
\makeatother

% other
\DeclareMathOperator*{\argmax}{arg\!\max}
\DeclareMathOperator*{\argmin}{arg\!\min}
\newcommand{\Dom}[1]{\operatorname{Dom}\pargs{#1}}
\newcommand{\sgn}[1]{\operatorname{sgn}\pargs{#1}}
\newcommand{\Tr}{\operatorname{Tr}}
\newcommand{\dd}{\mathop{}\!\mathrm{d}}
\newcommand{\Dd}[1]{\mathop{}\!\mathrm{d^#1}}

% probability
\DeclareMathOperator*{\Expval}{\mathbb{E}}
\newcommand{\EX}[2]{\Expval_{#1}\bargs{#2}}
\DeclareMathOperator*{\Prob}{Pr}
\renewcommand{\Pr}[2]{\Prob_{#1}\bargs{#2}}
\DeclareMathOperator*{\variance}{Var}

% morphisms
\newcommand{\Hom}[1]{\operatorname{Hom}\pargs{#1}}
\newcommand{\End}[1]{\operatorname{End}\pargs{#1}}
\newcommand{\Aut}[1]{\operatorname{Aut}\pargs{#1}}

% big O notation
\newcommand{\bigO}[1]{\calO\pargs{#1}}
\newcommand{\littleo}[1]{o\pargs{#1}}
\newcommand{\bigOmega}[1]{\Omega\pargs{#1}}
\newcommand{\littleomega}[1]{\omega\pargs{#1}}
\newcommand{\bigTheta}[1]{\Theta\pargs{#1}}
\newcommand{\poly}[1]{\operatorname{poly}\pargs{#1}}
\newcommand{\polylog}[1]{\operatorname{polylog}\pargs{#1}}
% with *, don't automatically size
\WithSuffix\newcommand\bigO*[1]{\calO\pargs*{#1}}
\WithSuffix\newcommand\littleo*[1]{o\pargs*{#1}}
\WithSuffix\newcommand\bigOmega*[1]{\Omega\pargs*{#1}}
\WithSuffix\newcommand\littleomega*[1]{\omega\pargs*{#1}}
\WithSuffix\newcommand\bigTheta*[1]{\Theta\pargs*{#1}}
\WithSuffix\newcommand\poly*[1]{\operatorname{poly}\pargs*{#1}}
\WithSuffix\newcommand\polylog*[1]{\operatorname{polylog}\pargs*{#1}}

% more math
\newcommand{\e}{\mathrm{e}}
\renewcommand{\i}{\mathrm{i}}
\newcommand{\U}{\mathrm{U}}
\renewcommand{\O}{\mathrm{O}}
\newcommand{\Sp}{\mathrm{Sp}}
\newcommand{\GL}{\mathrm{GL}}
\renewcommand{\Re}{\operatorname{Re}}
\renewcommand{\Im}{\operatorname{Im}}


```

{% endraw %}

{% include post-footer.html %}
