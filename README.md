# GGG-Synthesizer

The GGG-Synthesizer is an R Shiny application that generates multivariate synthetic data from a Gaussian likelihood with a Gaussian–Inverse-Wishart (GIW) prior. The app computes the posterior parameters in closed form, simulates synthetic datasets, and provides analytical disclosure-risk outputs under the “all-but-one” identification framework.

The tool is designed for methodological experimentation, teaching, and rapid evaluation of privacy–utility tradeoffs in multivariate normal synthesizers.

## Core functionality

The application provides:

### 1. Posterior inference  
Given real data \(X = \{\mathbf{x}_1,\dots,\mathbf{x}_n\}\) and GIW hyperparameters  
\((\mu_0, \kappa_0, \Lambda_0, \nu_0)\), the app computes the conjugate posterior  
\[
(\mu^{*}, \Sigma^{*}) \mid X \sim \mathrm{NIW}(\mu_n, \kappa_n, \Lambda_n, \nu_n)
\]
in closed form. Posterior parameters are displayed interactively.

### 2. Synthetic data generation  
- Users choose the number of synthetic datasets \(n_k\) and the number of posterior draws \(n_\theta\).  
- Synthetic datasets are generated from the posterior predictive Student-t distribution.  
- All generated data can be downloaded.

### 3. Disclosure-risk evaluation  
Implements the closed-form identification-risk expression derived for the GGG framework:
- Computes the distance measure  
  \(\mathcal{D}_s(\mathbf{x}^c_s, \mathbf{x}_i)\)  
  between the candidate outlier and synthetic points.
- Evaluates how the risk behaves as:
  - dimensionality increases
  - the number of synthetic datasets increases
  - the number of posterior draws increases.
- Includes 2D visual illustrations and violin plots.

### 4. Visual diagnostics  
- Scatterplots for the real data, posterior draws, and synthetic data.  
- Kernel density overlays.  
- Interactive selection of dimensions to plot.

## File structure



GGG-Synthetizer/
├─ app.R # Full Shiny application
├─ GGG-Synthetizer.Rproj # RStudio project file
└─ .Rhistory # R command history


## Requirements

R packages used in the app (as invoked inside `app.R`):

```r
install.packages(c(
  "shiny",
  "MASS",
  "mvtnorm",
  "ggplot2",
  "tidyverse",
  "gridExtra"
))

Running the app

Open the project in RStudio or set the working directory to the repository and run:

shiny::runApp("app.R")


The Shiny interface will open in your browser.

Intended use

The synthesizer is useful for:

Demonstrating conjugate Bayesian updating for multivariate normals

Comparing multiple synthetic-data release strategies

Teaching disclosure-risk concepts

Experimenting with how dimensionality affects identification risk

Reproducing the analytical results from the associated manuscript

Limitations

Restricted to multivariate Gaussian data

GIW prior only

No support yet for mixtures or non-Gaussian synthesizers

Not packaged as an R package

Roadmap

Add mixture synthesizers (Gaussian mixtures, copulas)

Add numerical utilities for high-d dimensions

Add reproducible examples and simulation notebooks

Add CI and automated tests

Optional: convert to an R package
