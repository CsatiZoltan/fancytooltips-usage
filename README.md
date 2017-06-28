# fancytooltips-usage
Installation and usage of the fancytooltips package



## Introduction

There are several packages available that make it possible to insert tooltips into LaTeX generated PDF files, see e.g. [fancytooltips](https://bitbucket.org/robert.marik/fancytooltips/), [cooltooltips](https://www.ctan.org/pkg/cooltooltips?lang=en), [ocgx](https://github.com/polgab/ocgx), and some simplistic solutions like INSERT THE ONE WITH A SIMPLE TEX FILE AT HOME. Some features of these packages:

- [cooltooltips](https://www.ctan.org/pkg/cooltooltips)
    - shows pretty basic tooltips and mouse hovering does not work, just mouse clicking
    - requires Adobe Reader
- [pdfcomment](https://www.ctan.org/pkg/pdfcomment)
    - as its name suggests, the tooltips are realized as comments
    - requires Adobe Reader
- [ocgx](https://www.ctan.org/pkg/ocgx)
    - highly customizable layers which show up or disappear on clicking
    - interoperability with TikZ
    - does not rely on Javascript -> can be used for other viewers than Acrobat Reader (e.g. Evince)
    - powerful (see e.g. [this demo](http://mirrors.ircam.fr/pub/CTAN/macros/latex/contrib/ocgx/demo-ocgx.pdf)) but has steep learning curve
- [fancytooltips](https://www.ctan.org/pkg/fancytooltips)
    - no need to modify the source .tex file for effects, just include the *fancytooltips* header; it will automatically cut the clickable references
    - possibility to include additional tooltips and animations manually (see the [examples](https://www.ctan.org/tex-archive/macros/latex/contrib/fancytooltips/examples))
    - requires *perl*, Adobe Reader and the packages *ocg*, *acrotex*



## Installation

Theoretically, on-the-fly package installation should work with MiKTeX, but I had so many problems with it that for the sake of fancytooltips, I installed the full MiKTeX.

1. Install the *fancytooltips* and the *acrotex* packages.
    - *fancytooltips* is part of both TeXlive and MiKTeX: https://www.ctan.org/pkg/fancytooltips?lang=en
    - *acrotex* is available in the MiKTeX package manager or can be manually downloaded from CTAN: https://www.ctan.org/pkg/acrotex?lang=en
2. Install the *ocg* package. For me, neither the *ocgx*, nor the *ocg-p* packages worked with *fancytooltips*, so we need to install the original ocg:
    - download ocg.sty (e.g. http://mirrors.ctan.org/graphics/asymptote/doc/ocg.sty)
    - create a directory called ocg in /MiKTeX_dir/tex/latex and put ocg.sty into it.
    - in MiKTeX Options, on the General tab, click on Refresh FNDB and on Update Formats
3. Install perl. The author of the fancytooltips recommends ActivePerl for Windows: http://www.activestate.com/activeperl. It is easy to manage the perl modules with it, what we will need in the next step
4. Open the Perl Package Manager and install the Config::IniFiles module.



## Usage

It is recommended to create an .ini file that holds your settings so that you don't have to modify fancy-preview.

Call fancy-preview from the command prompt:

	perl fancy-preview fileNameWithoutExtension -options

With the example files of this repository:

	perl fancy-preview mwe.tex --ini_file=settings.ini



## Using with *biber*

I modified the *fancy-preview* script to work with biber. However, it only works if the .bbl file has already been created. Therefore, first run `pdflatex-biber` and then the *fancy-preview_biber* script the same way as described above. Unfortunately, it does not extract the bibliography, only the references.



## Limitations

Currently there are some limitations of the fancy-preview script:

- it is hard-coded for bibtex and not for biber
- requires Adobe Reader/Acrobat
- cropping with *pdfcrop* can can result in (relatively) large file sizes as is mentioned in the [manual](http://ftp.oleane.net/pub/CTAN/macros/latex/contrib/fancytooltips/fancytooltips.pdf) too. You can use pdftk instead.
- environments (like figures) must float



## Useful links

http://tex.stackexchange.com/questions/82336/mouseover-events-in-beamer-hovering-on-eqref-and-a-comment-containing-the-orig



## Contribution

If you have solutions for the improvements above or any other recommendations, feel free to send a pull request.

If you find any problems with this tutorial, raise an issue.
