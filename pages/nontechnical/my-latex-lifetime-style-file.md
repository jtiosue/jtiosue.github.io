---
title: My LaTeX lifetime style file
comments: 14
---

{% include post-header.md %}

(Ongoing) Over the years, I've learned that LaTeX is really quite wonderful. Many have suggested that I have a "lifetime style file" that I add to my LaTeX documents with `\usepackage{lifetime.sty}`. So I created one, and will (probably) continue updating it as I go along. By the way, one of the things I most wish I knew about LaTeX a long time ago was the ability to separate documents into multiple files and compile them into one file via the `\input{}` command.


```latex
\usepackage[left=1in,right=1in,top=1in,bottom=1in]{geometry}
\usepackage{amsmath,amssymb,amsthm,amsfonts,bm,graphicx,physics,mathtools}
\usepackage[colorlinks,citecolor=blue,bookmarks=true]{hyperref}
\allowdisplaybreaks

\usepackage[style=numeric-comp,sorting=none]{biblatex}\renewbibmacro{in:}{}
% use with \addbibresource{filename1.bib,filename2.bib} then \printbibliography

% meta
\newcommand{\iosuename}{Joseph~T.~Iosue}
\newcommand{\iosueemail}{\href{mailto:jtiosue@umd.edu}{jtiosue@umd.edu}}
\newcommand{\UMD}{University~of~Maryland,~College~Park,~Maryland~20742~USA}
\newcommand{\iosueaffiliations}[1]{
    \ifnum#1=1
        Joint~Quantum~Institute,~\UMD
    \else 
        \ifnum#1=2 
            Joint~Center~for~Quantum~Information~and~Computer~Science,~\UMD
        \else 
            \iosueaffiliations{1},~\iosueaffiliations{2}
        \fi
    \fi
}

% for ``commenting out'' chunks of text 
\newcommand{\ignore}[1]{}
% for notes on the text 
\newcommand{\note}[1]{{\color{red} [#1]}}

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
\theoremstyle{definition}\newtheorem{example}[theorem]{Example}

% ref
\newcommand{\Equation}[1]{\eqref{eq:#1}}
\newcommand{\Section}[1]{Section~\ref{sec:#1}}
\newcommand{\Figure}[1]{Figure~\ref{fig:#1}}
\newcommand{\Table}[1]{Table~\ref{table:#1}}
\newcommand{\Definition}[1]{Definition~\ref{def:#1}}
\newcommand{\Example}[1]{Example~\ref{ex:#1}}
\newcommand{\Remark}[1]{Remark~\ref{re:#1}}
\newcommand{\Theorem}[1]{Theorem~\ref{thm:#1}}
\newcommand{\Claim}[1]{Claim~\ref{claim:#1}}
\newcommand{\Proposition}[1]{Proposition~\ref{prop:#1}}
\newcommand{\Lemma}[1]{Lemma~\ref{lem:#1}}
\newcommand{\Corollary}[1]{Corollary~\ref{cor:#1}}
\newcommand{\Conjecture}[1]{Conjecture~\ref{con:#1}}
\newcommand{\Observation}[1]{Observation~\ref{obs:#1}}
\newcommand{\Fact}[1]{Fact~\ref{fact:#1}}

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

% other
\DeclareMathOperator*{\argmax}{arg\!\max}
\DeclareMathOperator*{\argmin}{arg\!\min}

% brackets
\newcommand{\parentheses}[1]{\left(#1\right)}
\newcommand{\brackets}[1]{\left[#1\right]}
\newcommand{\curlybrackets}[1]{\left\{#1\right\}}
\newcommand{\angles}[1]{\left\langle #1\right\rangle}
\newcommand{\ceil}[1]{\left\lceil #1\right\rceil}
\newcommand{\floor}[1]{\left\lfloor #1\right\rfloor}

% probability
\DeclareMathOperator*{\Expval}{\mathbb{E}}
\newcommand{\EX}[2]{\Expval_{#1}\!\brackets{#2}}

% morphisms
\newcommand{\Hom}[1]{\text{Hom}\!\parentheses{#1}}
\newcommand{\End}[1]{\text{End}\!\parentheses{#1}}
\newcommand{\Aut}[1]{\text{Aut}\!\parentheses{#1}}

% big O notation
\newcommand{\bigO}[1]{\calO\!\parentheses{#1}}
\newcommand{\littleo}[1]{o\!\parentheses{#1}}
\newcommand{\bigOmega}[1]{\Omega\!\parentheses{#1}}
\newcommand{\littleomega}[1]{\omega\!\parentheses{#1}}
\newcommand{\bigTheta}[1]{\Theta\!\parentheses{#1}}
\newcommand{\poly}[1]{\text{poly}\!\parentheses{#1}}
\newcommand{\polylog}[1]{\text{polylog}\!\parentheses{#1}}
```


{% include post-footer.html %}
