This is PaTeX, my personal TeX format. It is

* a learning experience for me, as I get to know how basic convenience mechanisms can be implemented in TeX _in principle_;
* a format I can use to create specialized documents, as I know exactly what which macro does, allowing me full control over the document;
* potentially useful as a demonstration of or even source of inspiration for how to do things in virgin TeX.

It is **not**

* any close to a fully fledged format offering the capabilities of e.g. LaTeX; in fact, it doesn't even contain all the `plain.tex` macros, yet;
* an example of high quality TeX coding;
* well-documented, user-friendly, or bug-free.

Following is some documentation, especially for my future self. Feel free to use it as you wish, though.

# Installation

1. Clone this repository into `~/texmf/tex/`.
1. Execute the bash script `ini/makepatex`. This creates the `fmt` files and puts them into `~/texmf/web2c/{tex,pdftex,xetex,luatex}/` only if the respective directory exists.
1. Execute the bash script `bin/link`. This creates the binaries and links them to files in `~/bin/`, where I store my user bash scripts.

# Usage

After the above installation procedure, the following binaries are available:

binary|running on|default output
---|---|---
`virpatex`|Knuth's TeX|`dvi`
`epatex`|e-TeX|`dvi`
`pdfpatex`|pdfTeX|`pdf`
`luapatex`|LuaTeX|`pdf`
`xepatex`|XeTeX|`pdf`
`patex`|{,pdf,Xe}TeX|`pdf`/`dvi`

The invoked engine for `patex` depends on the first line of the file to be compiled. It **must** be one of

    %\english
    %\europe
    %\world

where

* `%\english` invokes Knuth's TeX: Only US American hyphenation, `ASCII` input and `OT1` encoded fonts are supported out of the box and output is `dvi` only.
* `%\europe` invokes pdfTeX with e-TeX and extensions. The supported hyphenation patterns are found in the `language.def` file of the TeX distribution; `UTF-8` input for characters based on the Latin alphabet and `T1` (Cork) encoded fonts are supported.
* `%\world` invokes XeTeX. In addition to the above hyphenation patterns, `UTF-8` input and `OTF/TTF` fonts are supported.

Apart from the first line, the document can have the same structure as any `plain` TeX file, apart from `\bye`, which is called `\thx` in PaTeX for the sake of incompatibility.

# Features

There aren't many, but there will probably be more in the future. The core depends on the binary used; which files are included in each case is managed by `patex.ini`.

`.tex` file|provides
---|---
`patex-base`|catcode setup, register allocation, logos
`patex-api`|macro programming tools
`patex-enc`|provides `\encode T1` and `\encode OT1` font encoding, limited `UTF-8` input encoding for 8-bit engines and shorthands to access the glyphs of the fonts
`patex-mathenc`|mathematics font glyphs shorthands
`patex-parameters`|TeX's parameters
`patex-layout`|macros for setting the page dimensions and margins, notably `\usepaper{a4}`
`patex-font`|basic font selection tools, with `\usefont` allowing to load a font `x` with a corresponding `patex/pkg/patex-fonts/patex_font_x.tex` file
`patex-mac`|basic formatting macros
`engine/epatex`|nearly identical to `etex.src`, sets up `\uselanguage` and improved register allocation
`engine/pdfpatex`|nearly identical to `pdfconfig.tex`, basic `pdf` settings
`engine/luapatex`|nearly identical to `luatex.ini`, LuaTeX support
`engine/xepatex`|nearly identical to `xetex.ini`, support for unicode and line-breaking for CJK

There are also some packages to be `\input` available in `pkg`:

package|provides
---|---
`p-microtype`|interface to pdfTeX's micotypography features, like LaTeX's microtype package but much more primitive
`p-typewriter`|lets a document appear as if written on an old typewriter, with consistent offsets for each character, random boldness, randomly squeezed in letters and a few other things; it makes all letters active so it will only allow one-letter control sequences to be used after it was loaded
`texmachine`|provides `\parse|...|`, which prints a representation of TeX's token scanning mechanism of the input
`patex-fonts`|each file sets up the `\rm`, `\bf`, `\it` etc. commands available for a font when loaded with `\usefont`

# Licence

This work is in the public domain.
