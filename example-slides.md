---
author:
- Matthias Laugwitz\
- Jann Launer\
- Guido Pleßmann
short-author: 
- Guido Pleßmann
title: The RLI \LaTeX{} beamer theme
subtitle: ...finally overcoming MS Powerpoint
titlepage-note: |
  This is a the note that goes on the title page. This talk is to be 
  given at Doing DH.
institute: Reiner Lemoine Institut
classoption: aspectratio=169
date: \today
theme: rli
header-includes:
- |
  \newcommand{\tel}{+49 (0)30 1208 434 72}
  \newcommand{\email}{guido.plessmann@rl-institut.de}
  \newcommand{\twitter}{\href{https://twitter.com/gplssm}{@gplssm}}
  \newcommand{\finalstatement}{Enjoy stating a final statement ;-)}
...

# One-line title

~~~ latex
\begin{frame} 
\frametitle{One-line title} 
\end{frame}
~~~

# Title with subtitle

\framesubtitle{Be more presice using a subtitle}

~~~ latex
\begin{frame} 
\frametitle{Title with subtitle} 
\framesubtitle{Be more presice using a subtitle}
\end{frame}
~~~

# Use lists and enumerated lists

- item a
- item c
- item b
	#. item 1
	#. item 2
	#. item 3

# Descriptions

\begin{description}[A]
  \item[A] A?
  \item[B] B?
  \item[C] C?
\end{description}

# Forget about \LaTeX{} , use pandoc!

## Pandoc

Multi text-format converter with CLI

* .tex <-> .md <-> html <-> pdf <-> ePub <-> .docx <-> ... 


## Command to build these slides

~~~ bash
 pandoc -t beamer -o example-slides.pdf example-slides.md
~~~

with frontmatter

~~~ yaml
---
- title: <Title>
- ...
- theme: rli
---
~~~

---

Frame with no title

# Warum ist ein \LaTeX{} template gut?

#. Layout und Inhalt sind getrennt!
#. Gute Defaults
#. Source file (.tex oder .md) ist eine Textdatei
#. Maschinenlesbar und mit git versionierbar
#. Auf GitHub zu verwalten, weil kein BLOB
#. Markdown nutzen wir auch in Redmine

# Figures

# Tables

* Simple table
* More complex
* Maybe an advanced table
* It's easy to convert structured data into Markdown table syntax: on the example of JSON

# Blocks

\begin{block}{Title}
Here you can put your content
\end{block}

in Markdown you simply use

``` markdown
## Markdown block header

Markdown block content
```

to achieve the same, see

## Markdown block header

Markdown block content

# Using the default last slide

## Latex

``` latex
\begin{frame}[plain]{}

\insertendpagecontent

\end{frame}
```

## Markdown

``` markdown
# {.plain}

\insertendpagecontent
```

# {.plain}

\insertendpagecontent
