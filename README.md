The RLI corporate identidy implemented as a theme for Latex document class [beamer](https://en.wikibooks.org/wiki/LaTeX/Presentations). Usable with both, LaTeX and Markdown through [pandoc](https://pandoc.org/). Here are some [example slides](https://speakerdeck.com/gplssm/rli-latex-beamer-example-slides)  

![](img/example_slides.gif)

# Installation

You need to have some Latex packages installed. Linux users may use

```
sudo apt install texlive
sudo apt install texlive-xetex # to use unicode-aware xelatex
sudo apt install texlive-latex-recommended # for latex beamer
sudo apt install texlive-fonts-extra # maybe required for fonts
```

## Font

The theme uses the RLI house font **Nunito Sans** (Corporate Design 2025), loaded via
`fontspec`, so slides must be built with **XeLaTeX** (or LuaLaTeX) — not `pdflatex`.
The font is **not** part of this repository and must be installed on your system.
Download Nunito Sans (e.g. from [Google Fonts](https://fonts.google.com/specimen/Nunito+Sans),
or the RLI Corporate Design package), which provides the required faces — Regular, Bold,
Italic, Bold Italic, and ExtraBold (used for headings) — then install them, e.g. on Linux:

```
mkdir -p ~/.local/share/fonts
cp NunitoSans-*.ttf ~/.local/share/fonts/   # from your download
fc-cache -f
```

Verify they are found with `fc-list | grep -i nunito`.

## Extra packages for markdown (pandoc)

```
sudo apt install pandoc
```

When using pandoc, it's recommended to use a version >2.0. Ubuntu/Debian user should know that pandoc from official sources might be outdated. Consider to install a [newer version](https://pandoc.org/installing.html).

For using citations with pandoc pandoc-citeproc is required

```
sudo apt install pandoc-citeproc
```


# Building the example slides

You need the `.sty` files and the `img/` folder right next to your `slides.md` file.

Recommended workflow
  - Have the clone of [https://github.com/rl-institut/beamer_theme/](https://github.com/rl-institut/beamer_theme/)
    
    ```
    git clone git@github.com:rl-institut/beamer_theme.git
    ```
  - Keep it up-to-date
  - Copy required files to your slides path

    ```
    cp -r beamer_theme/img/ beamer_theme/*.sty <path-of-slide.md> 
    ```

## LaTeX

Make sure you have following two lines in the preamble

```
\documentclass[aspectratio=169]{beamer}

\usetheme{rli}
```

Build example slides from `.tex` file 

```
xelatex example-slides.tex
```

and then: happy building your own slides :tada:.

See the `example_slides.tex` for some hints on how to create slides with latex beamer.

If [bibtex](https://de.wikipedia.org/wiki/BibTeX) citations are used, run the following commands for correctly processing newly added citations

```
xelatex example-slides.tex
bibtex example-slides.aux
xelatex example-slides.tex
xelatex example-slides.tex
```
## Markdown (with Pandoc)

When using Markdown (`.md`) files for creating slides, include the following in the front matter

```
---
- title: <Title>
- ...
- theme: rli
---
```

Convert `.md` files to beamer PDF slides by

```
pandoc -t beamer --listings --pdf-engine=xelatex -o example-slides.pdf example-slides.md
```

The `--listings` flag makes pandoc typeset code blocks with the `listings` package
(line numbers, syntax colors) matching the LaTeX build, instead of its default
highlighter. The corresponding `\lstset` lives in the front matter's `header-includes`.

To enable processing of citations, set `bibliography: bib/example.bib` in the front
matter and add `--citeproc`

```
pandoc -t beamer --listings --citeproc --pdf-engine=xelatex -o example-slides.pdf example-slides.md
```

Note: `--citeproc` requires pandoc ≥ 2.11. On older pandoc, replace it with
`--filter pandoc-citeproc` (install the separate `pandoc-citeproc` package). If you
use **pandoc version <2.0**, also replace `--pdf-engine` by `--latex-engine=`.

Have a look into `example_slides.md` for details and examples.

### Bibliography style

For a custom reference list format, you can download a
[Citation Style Language](https://citationstyles.org/) (CSL) file from
[zotero](https://www.zotero.org/styles) to your `./bib` directory. Activate the
style by passing the option `--csl bib/<STYLE_FILE>.csl` to pandoc, e.g.
`--csl bib/chicago-author-date-de.csl`.

To generate a full bibliography, regardless of whether the entries were
referenced on the slides or not, use the option `nocite: '@*'` in the header
of the front matter.

# Contributing

Contributions are welcome! Read [CONTRIBUTING](https://github.com/rl-institut/beamer_theme/blob/master/CONTRIBUTING.md) for developing workflow.
If you don't know how to help, see issue for upcoming release.
