# How to use?

## Installation

You need to have `texlive-xetex` installed.

```
texlive-xetex
```


## Building the example slides

Clone the Repository (aka. download the files) and run

```
pandoc -t beamer --latex-engine=xelatex -o example-slides.pdf example-slides.md 
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
