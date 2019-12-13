---
author:
- Guido Pleßmann
- Jann Launer
- Matthias Laugwitz
title: The RLI \LaTeX{} beamer theme
subtitle: ...finally overcoming MS Powerpoint
institute: Reiner Lemoine Institut
classoption: aspectratio=169
date: \today
theme: rli
urlcolor: rlilinkcolor
header-includes:
- |
  \newcommand{\tel}{+49 (0)30 1208 434 72}
  \newcommand{\email}{guido.plessmann@rl-institut.de}
  \newcommand{\twitter}{\href{https://twitter.com/gplssm}{@gplssm}}
  \newcommand{\finalstatement}{Enjoy stating a final statement ;-)}
  \tikzset{
  invisible/.style={opacity=0},
  visible on/.style={alt={#1{}{invisible}}},
  alt/.code args={<#1>#2#3}{%
    \alt<#1>{\pgfkeysalso{#2}}{\pgfkeysalso{#3}} % \pgfkeysalso doesn't change the path
  },
  }
---

# A new frame

Create a new frame with title and content

~~~ markdown
# A new frame

With content in it's body.
~~~


# Use formatting syntax

The _quick_ **brown** fox ^jumps^ ~over~ the `lazy` ``dog``~~, not the cat~~.

You can also quote it

> The quick brown fox jumps over the lazy dog, not the cat.

Moreover, you can simply write \LaTeX{} code in .md files.


# Use lists and enumerated lists

- item a
  - item a.1
    - item a.1.a
    - item a.1.b
	
#. item 1
   #. item a
#. item 2
#. item 3
   - mix
   - it

# Descriptions

Distributed Energy Resource
 : Electrical power generation or storage located at or near the point of use, as well as demand side measures.

Distributed Generation
 : Electric power generation located at or near the point of use.

Distributed Power
 : Electrical power generation or storage located at or near the point of use.

\footnotesize Content stolen from [ACEEE glosarry](https://aceee.org/glossary_data).

# Insert images

\center
![](img/createria-ZYu6P9-Glic-unsplash_resized.jpg){ width=75% }

# Presenting code

~~~ python
import requests
import pandas as pd
from tabulate import tabulate

df = pd.DataFrame(requests.get('http://openenergy-platform.org/api/v0\
  /schema/supply/tables/bnetza_eeg_anlagenstammdaten/rows/?limit=100').json())

df = df[[
  '4.11_bundesland',
  '4.1_energieträger', 
  '4.2_installierte_leistung',
  '4.16_name_des_netzbetreibers']]
df.columns = ["Federal state", "Technology", "Inst. Power", "Grid operator"]

print(tabulate(df.head(10), tablefmt="pipe", headers="keys"))
~~~

# Tables

|    | Federal state       | Technology   |   Inst. Power | Grid operator                       |
|---:|:--------------------|:-------------|--------------:|:------------------------------------|
|  0 | Niedersachsen       | Biomasse     |           366 | Avacon AG                           |
|  1 | Bayern              | Biomasse     |           380 | Bayernwerk AG                       |
|  2 | Bayern              | Wasserkraft  |             6 | Bayernwerk AG                       |
|  3 | Hessen              | Biomasse     |           380 | EnergieNetz Mitte GmbH              |
|  4 | Bayern              | Wind Land    |          3050 | Bayernwerk AG                       |
|  5 | Nordrhein-Westfalen | Biomasse     |           400 | Westfalen Weser Netz GmbH           |
|  6 | Nordrhein-Westfalen | Biomasse     |          1200 | Westfalen Weser Netz GmbH           |
|  7 | Schleswig-Holstein  | Wind Land    |          2000 | Schleswig-Holstein Netz AG          |
|  8 | Hessen              | Biomasse     |           400 | EnergieNetz Mitte GmbH              |
|  9 | Bayern              | Biomasse     |          1000 | MDN Main-Donau Netzgesellschaft mbH |

# Blocks

## Block header

Block content

# Use columns to organize your content

:::::: {.columns}
::: {.column  width=55%}
\includegraphics[width=\textwidth]{example-image-a}
:::

::: {.column  width=45%}
>- Explain
>- what's
>- to
>- see
:::
::::::

# Aligning images

# GIFs

A cat gif

---

Frame with no title

# {.plain }

...or a plain one, even without footer.

# Drawing with Tikz: animated energy system block diagram

:::::: {.columns}
::: {.column  width=45%} 
\begin{tikzpicture}

\tikzstyle{icon} = [inner sep=0pt];
\tikzstyle{flow} = [ultra thick, inner sep=0pt];

\coordinate (busTop) at (0.5\paperwidth,0.8\paperheight);
\coordinate (busBottom) at (0.5\paperwidth,0.3\paperheight);

\node (elecbus) at ($(busBottom) - (0,.5)$) {Household busbar};
\draw[line width=4pt](busTop) -- (busBottom);


\node[icon,draw,very thick, rounded corners=0.5ex, inner sep=3pt,visible on=<5->](dsm) at ($(busTop)!0.5!(busBottom) - (1,0)$) {{\visible<5->{\includegraphics[width=.8cm]{img/noun_filter_1653638.pdf}}}};
\node[icon](demand) at ($(busTop)!0.5!(busBottom) - (2.5,0)$) {{\visible<2->{\includegraphics[width=1.1cm]{img/Verbraucher_Haushalt_Strom.pdf}}}};
\node[icon](grid) at ($(busTop)!0.7!(busBottom) + (1,0)$) {{\visible<4->{\includegraphics[width=1.1cm]{img/Transport_Strom.pdf}}}};
\node[icon](pv) at ($(busTop)!0.3!(busBottom) + (1,0)$) {{\visible<3->{\includegraphics[width=1.1cm]{img/Stromerzeuger_Photovoltaik_Dachanlage.pdf}}}};

\draw[<-,flow, visible on=<5->](dsm) -- ($(busTop)!0.5!(busBottom)$);
\draw[->,flow, visible on=<5->](dsm) -- (demand);
\draw[<-,flow, visible on=<4->] ($(busTop)!0.7!(busBottom) + (2pt,0)$) -- (grid);
\draw[<-,flow, visible on=<3->] ($(busTop)!0.3!(busBottom) + (2pt,0)$) -- (pv);


\end{tikzpicture}
:::

::: {.column  width=40%}
**Assuming we have a household including**

\begin{itemize}
\item<2-> Demand
\item<3-> PV
\item<4-> Grid connection
\item<5-> Demand-side management unit
\end{itemize}

:::
::::::


# How to use the theme

- You need the `.sty` files and the `img/` folder right next to your `slides.md` file
- Recommended workflow
  - Have the clone of [https://github.com/rl-institut/beamer_theme/](https://github.com/rl-institut/beamer_theme/)
    
    ~~~ bash
    git clone git@github.com:rl-institut/beamer_theme.git
    ~~~
  - Keep it up-to-date
  - Copy required files to your slides path

    ~~~ bash
    cp -r beamer_theme/img/ beamer_theme/*.sty <path-of-slide.md> 
    ~~~


# Command to build these slides

~~~ bash
 pandoc -t beamer--pdf-engine=xelatex -o example-slides.pdf example-slides.md
~~~

with frontmatter

~~~ yaml
---
- title: <Title>
- ...
- theme: rli
---
~~~

# Information must be provided in markdown header

Requires the following \LaTeX{} code in `- header-includes`

~~~ latex
---
header-includes:
- |
  \newcommand{\tel}{+49 (0)30 1208 434 72}
  \newcommand{\email}{guido.plessmann@rl-institut.de}
  \newcommand{\twitter}{\href{https://twitter.com/gplssm}{@gplssm}}
  \newcommand{\finalstatement}{Enjoy stating a final statement ;-)}
---
~~~

# Find help

- Pandoc manual: [https://pandoc.org/MANUAL.html](https://pandoc.org/MANUAL.html)
- Useful overview of commands for formatting with Markdown and pandoc: [http://www.flutterbys.com.au/stats/tut/tut17.3.html](http://www.flutterbys.com.au/stats/tut/tut17.3.html)
- Theme repository: [https://github.com/rl-institut/beamer_theme](https://github.com/rl-institut/beamer_theme)
- Demo slides (compiled example slides.md): ...

# Using the default last slide


``` markdown
# {.plain}

\insertendpagecontent
```

# {.plain}

\insertendpagecontent
