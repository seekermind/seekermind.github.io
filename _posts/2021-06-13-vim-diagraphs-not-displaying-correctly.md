---
layout: post
title: Vim special characters(diagraphs) not displaying correctly
description: I have been facing a wierd problem of vim no beeing able render special characters (diagraphs). Heres how to fix this.
tags: vim font
---

You need to do two things:
1. set UTF-8 encoding
2. make sure vim uses a font that includes glyphs for the Unicode characters

## UTF-8 encoding

Put the following line in your `vimrc`:

```
set encoding=utf-8
```

If you use terminal Vim, you also need to configure your terminal emulator to use UTF-8 encoding. The way to do that depends on your terminal emulator.

#### Check if your terminal emulator supports utf-8 encoding
Really, the surefire way to test is to download a [text file](https://www.cl.cam.ac.uk/~mgk25/ucs/examples/) and cat it in the terminal and see if everything looks ok.
You can also check if these works: Α α, Β β, Γ γ, Δ δ, Ε ε, Ζ ζ, Η η, Θ θ, Ι ι, Κ κ, Λ λ, Μ μ, Ν ν, Ξ ξ, Ο ο, Π π, Ρ ρ, Σ σ/ς, Τ τ, Υ υ, Φ φ, Χ χ, Ψ ψ, and Ω ω.

## Setting vim's font
You need a font that
1. is monospace (fixed width)
2. includes the Unicode characters that you use

[DejaVu Sans Mono](https://www.fontmirror.com/dejavu-sans-mono) is fine for me. DejaVu is also available in `pacman` repo:

```
sudo pacman -S ttf-dejavu
```

The way to tell Vim which font to use depends on whether you are using a GUI Vim, such as gVim or MacVim, or terminal Vim. If you use terminal Vim, specify the font in your terminal emulator’s configuration. I use st. In that i would go to st's config.h file and add a line 

```c
static char *font = "DejaVu Sans Mono:pixelsize=12:antialias=true:autohint=true";
```

If you use any GUI version then you are of your own, I don't like GUI.


Note:
Run `:dig` in vim commad line to get list of diagraphs.
