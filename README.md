The RLI Latex beamer theme. 

![](img/example_slides.gif)

# How to use

## Installation

You need to have `texlive-xetex` installed.

```
texlive-xetex
```

When using pandoc, it's recommended to use a version >2.0. Ubuntu/debian user should know that pandoc from official sources might be outdated. Consider to install a [newer version](https://pandoc.org/installing.html).

For using citations with pandoc pandoc-citeproc is required

```
sudo apt install pandoc-citeproc
```


## Building the example slides

Clone the Repository (aka. download the files) and run

```
pandoc -t beamer --latex-engine=xelatex -o example-slides.pdf example-slides.md 
```

To enable processing of citations use

```
pandoc -t beamer --filter pandoc-citeproc --bibliography bib/example.bib --pdf-engine=xelatex -o example-slides.pdf example-slides.md
```

## Use the theme for your own slides

Clone the Repository (aka. download the files) and copy `*.sty` files  and the `img/` folder to your project folder (right next to your `.tex` file).

Make sure you have following two lines in the preamble

```
\documentclass[aspectratio=169]{beamer}

\usetheme{rli}
```
and then: happy building your slides :tada:.

See the example slides for some hints on how to create slides with latex beamer.
