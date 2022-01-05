---
title: My LaTeX lifetime style file
comments: 14
---

{% include post-header.md %}

(Updated 25 Aug 2021) Over the years, I've learned that LaTeX is really quite wonderful. Many have suggested that I have a "lifetime style file" that I add to my LaTeX documents with `\usepackage{lifetime.sty}`. So I created one, and will (probably) continue updating it as I go along. By the way, one of the things I most wish I knew about LaTeX a long time ago was the ability to separate documents into multiple files and compile them into one file via the `\input{}` command. Or, even better, is the `\import{path}{file}` command, which updates the path in the import so you can use relative paths in your document.

{% raw %}

```latex
\usepackage[left=1in,right=1in,top=1in,bottom=1in]{geometry}
\usepackage{amsmath,amssymb,amsthm,amsfonts,bm,graphicx,braket,mathtools,import}
\allowdisplaybreaks

% newline for new paragraph
% \usepackage[parfill]{parskip}

\usepackage[style=numeric-comp,sorting=none]{biblatex}\renewbibmacro{in:}{}
% use with \addbibresource{filename1.bib} then \printbibliography

% make bib font smaller
% \renewcommand*{\bibfont}{\small}

% ONLY FOR DRAFTING, COMMENT THIS OUT FOR THE FINAL DOCUMENT.
\usepackage{showkeys}

% for dummy words, use with \lipsum or \lipsum[50], etc.
\usepackage{lipsum}

% meta
\newcommand{\iosuename}{Joseph~T.~Iosue}
\newcommand{\iosueemail}{\href{mailto:jtiosue@umd.edu}{jtiosue@umd.edu}}
\newcommand{\UMD}{University~of~Maryland,~College~Park,~Maryland~20742,~USA}
\newcommand{\JQI}{Joint~Quantum~Institute,~\UMD}
\newcommand{\QUICS}{Joint~Center~for~Quantum~Information~and~Computer~Science,~\UMD}
\newcommand{\iosueaffiliations}[1]{
    \ifnum#1=1
        \JQI
    \else 
        \ifnum#1=2 
            \QUICS
        \else 
            \iosueaffiliations{1},~\iosueaffiliations{2}
        \fi
    \fi
}

% to label equations by section, e.g. equation 1.3, 2.5, etc.
% \numberwithin{equation}{section}

% for ``commenting out'' chunks of text 
\newcommand{\ignore}[1]{}
% for notes on the text 
\usepackage{suffix}
\newcommand{\note}[1]{{\color{red} [#1]}}
\WithSuffix\newcommand\note*[1]{{\color{red} #1}}

% supposed to be loaded last
\usepackage[colorlinks,citecolor=blue,bookmarks=true]{hyperref}

% needs to be loaded after hyperref
\usepackage[capitalize]{cleveref}

% theorems and etc.
\newtheorem{theorem}{Theorem}[section]
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
\newcommand{\angles}[1]{\left\langle #1\right\rangle}
\newcommand{\ceil}[1]{\left\lceil #1\right\rceil}
\newcommand{\floor}[1]{\left\lfloor #1\right\rfloor}
\renewcommand{\set}{\curlybrackets}
\newcommand{\abs}[1]{\left\lvert #1 \right\rvert}
\newcommand{\norm}[1]{\left\lVert #1 \right\rVert}

% other
\newcommand{\pargs}[1]{\!\parentheses{#1}}
\newcommand{\bargs}[1]{\!\brackets{#1}}
\newcommand{\cbargs}[1]{\!\curlybrackets{#1}}
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

% morphisms
\newcommand{\Hom}[1]{\mathrm{Hom}\pargs{#1}}
\newcommand{\End}[1]{\mathrm{End}\pargs{#1}}
\newcommand{\Aut}[1]{\mathrm{Aut}\pargs{#1}}

% big O notation
\newcommand{\bigO}[1]{\calO\pargs{#1}}
\newcommand{\littleo}[1]{o\pargs{#1}}
\newcommand{\bigOmega}[1]{\Omega\pargs{#1}}
\newcommand{\littleomega}[1]{\omega\pargs{#1}}
\newcommand{\bigTheta}[1]{\Theta\pargs{#1}}
\newcommand{\poly}[1]{\operatorname{poly}\pargs{#1}}
\newcommand{\polylog}[1]{\operatorname{polylog}\pargs{#1}}

% more math
\newcommand{\e}{\mathrm{e}}
\renewcommand{\i}{\mathrm{i}}
\newcommand{\U}{\mathrm{U}}
\renewcommand{\O}{\mathrm{O}}
\newcommand{\Sp}{\mathrm{Sp}}
\newcommand{\GL}{\mathrm{GL}}


```

{% endraw %}

{% include post-footer.html %}
