# Bachelor's Thesis

This repository contains the LaTeX source files for my bachelor's thesis in
Computer Engineering at the University of Brescia.

## Thesis

**Title:** Simulation-based evaluation of a 5G-V2X protocol for safe platoon
dismantling

**Author:** Alex Marchi

**Academic year:** 2024/2025

The thesis studies the reliability of vehicular communications in platooning
scenarios. In particular, it focuses on how a platoon can be safely dismantled
when communication quality degrades.

The work takes SafeSwitch as a reference mechanism and evaluates its behavior in
a modern simulation environment based on OMNeT++, Veins, Plexe, SUMO, and
Simu5G. The main contribution is the reconstruction and update of the
experimental setup, including the migration of the cellular component from
SimuLTE to Simu5G.

## Repository Structure

- `main.tex` is the main LaTeX entry point.
- `frontespice.tex` contains the title page.
- `summary.tex` contains the thesis summary.
- `body.tex` includes the main chapters.
- `chapters/` contains the thesis chapters and appendix.
- `images/` contains figures and graphical assets.
- `bibliography.bib` contains the bibliography.
- `template/` contains the original thesis template material.

## Building the Document

The project uses LaTeX with `biblatex` and `biber`.

If `latexmk` is available, the document can be built with:

```sh
latexmk -pdf main.tex
```

Alternatively, compile it manually with:

```sh
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

The generated PDF and auxiliary LaTeX files are ignored by Git.

## Language

The thesis is written in Italian, while this README is provided in English for
repository documentation.
