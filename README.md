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

Note: If you don't want to litter your system with the countless fonts from `texlive-fonts-extra` (a full list of the
Ubuntu package can be found [here](https://packages.ubuntu.com/xenial/texlive-fonts-extra)), you can get single
fonts by installing the specific system package. E.g. to install Roboto, use

```
sudo apt install fonts-roboto-hinted
```

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
pandoc -t beamer --pdf-engine=xelatex -o example-slides.pdf example-slides.md 
```

To enable processing of citations use

```
pandoc -t beamer --filter pandoc-citeproc --bibliography bib/example.bib --pdf-engine=xelatex -o example-slides.pdf example-slides.md
```

Note: If you use **pandoc version <2.0**, replace `--pdf-engine` by `--latex-engine=` to process the Markdown file.

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
