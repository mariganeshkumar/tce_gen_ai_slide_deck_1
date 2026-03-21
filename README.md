# TCE Gen AI Slide Deck

This repository contains the LaTeX source code for the "Foundations of Deep Learning & the Emergence of Generative AI" slide deck.

## Compilation Instructions

The slide deck is compiled using **[Tectonic](https://tectonic-typesetting.github.io/)**, a modern and lightweight TeX engine that automatically downloads required packages on-demand.

### Prerequisites

You need `tectonic` installed on your system. On macOS (with Homebrew), you can install it using:

```bash
brew install tectonic
```

### Compiling the Slides

To generate the PDF, run the following command in the root of the repository:

```bash
tectonic main.tex
```

This will produce a `main.pdf` file in the same directory.

## Features

- **Beamer & Metropolis Theme**: Professional and clean presentation style.
- **TikZ Diagrams**: Custom figures for probabilistic modeling, model capabilities, and neural network architectures.
- **Syntactic Highlighting**: Source code examples using the `listings` package.

## Project Structure

- `main.tex`: The primary LaTeX source file.
- `main.pdf`: The compiled presentation (ignored by git).
- `images/`: Contains graphics (`image.png`, `image2.png`) used in the slides.
- `hands-on/`: Contains Jupyter notebooks (`Perceptron_Hands_ON.ipynb`) for the hands-on sessions.

---
*Note: This project was originally imported from Overleaf and has been optimized for local compilation using Tectonic.*
