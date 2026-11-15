# emitter-zpl-tracking

How precisely can the position of a narrow spectral line be read from noisy,
low-count spectra, and which method gets closest to the theoretical limit?

The test case is the zero-phonon line (ZPL) of a single quantum emitter
recorded on a CCD spectrometer at short exposure times. All results in this
repository come from simulated spectra with a known ground truth.

## What is compared
Methods to estimate the line position:
- Brightest pixel (argmax)
- Three-point parabolic interpolation
- Centroid (centre of mass)
- Non-linear least-squares fit (`scipy.optimize.curve_fit`)
- Maximum-likelihood fit for mixed shot and read noise
- Batched fits on GPU (PyTorch)
- Classical machine-learning regressors (scikit-learn)
- Neural networks trained on simulated spectra (PyTorch)
- A neural network trained without labels, through a physics model of the
  spectrum in its loss

Every method is compared with the Cramér–Rao lower bound, the best precision
an unbiased estimator can reach.

## Scope and prior work
Sub-pixel peak localisation is a mature field. This is a learning project
that applies known methods to one measurement regime. It does not claim a
new method. Work it builds on:
- Mortensen et al., Nature Methods 7, 377 (2010), doi:10.1038/nmeth.1447
- Smith et al., Nature Methods 7, 373 (2010), doi:10.1038/nmeth.1449
- Anderson & King (2000), arXiv:astro-ph/0006325
- Lenz & Ayres, PASP 104, 1104 (1992), doi:10.1086/133096
- Przybylski et al. (Gpufit), Scientific Reports 7, 15722 (2017),
  doi:10.1038/s41598-017-15313-9
- Negri et al., Sensors 11, 3466 (2011), doi:10.3390/s110403466
- Raissi, Perdikaris & Karniadakis, Journal of Computational Physics 378,
  686 (2019), doi:10.1016/j.jcp.2018.10.045

## Simulation assumptions
- The line on the detector is the instrument's line-spread function,
  integrated over each pixel (Gaussian by default; other shapes are tested).
- Noise is Poisson shot noise plus Gaussian read noise, converted to
  integer counts.
- Spectra are stored as two columns (wavelength, intensity), one spectrum
  after another.
- Signal level, line width and noise are swept over ranges. No parameter is
  fitted to unpublished data.

## Progress
| Module | Content | Main tools | Status |
|---|---|---|---|
| 1 | Spectrum simulator, classical estimators, Cramér–Rao bound | NumPy, SciPy, pytest | Planned |
| 2 | Maximum-likelihood fit and robustness tests | SciPy | Planned |
| 3 | Classical machine learning: regression, classification, PCA | scikit-learn | Planned |
| 4 | Batched fits on GPU with automatic differentiation | PyTorch | Planned |
| 5 | Neural networks (1D CNN) with uncertainty output | PyTorch | Planned |
| 6 | Training through a physics model of the spectrum (no labels) | PyTorch | Planned |
| 7 | Physics-informed neural networks: damped oscillator, then a two-level emitter with dephasing | PyTorch, QuTiP | Planned |
| 8 | Streamlit demo and short report | Streamlit | Planned |

Module 7 addresses a different problem from modules 1–6 and may move to its
own repository.

## Learning resources used
- Inria, "Machine learning in Python with scikit-learn":
  https://inria.github.io/scikit-learn-mooc/
- PyTorch, "Learn the Basics":
  https://docs.pytorch.org/tutorials/beginner/basics/intro.html
- B. Moseley, "So, what is a physics-informed neural network?":
  https://benmoseley.blog/my-research/so-what-is-a-physics-informed-neural-network/
- QuTiP tutorials: https://qutip.org/qutip-tutorials/
- NVIDIA PhysicsNeMo: https://developer.nvidia.com/physicsnemo

## Background and acknowledgement
This project was inspired by, and builds on the public work of:

> P. Maan et al., "Anticipating decoherence in quantum systems",
> *Nature Communications* 17, 8239 (2026).
> https://doi.org/10.1038/s41467-026-72829-3

Public data and code from that study (CC BY 4.0):
- https://doi.org/10.5281/zenodo.19455550
- https://doi.org/10.5281/zenodo.20192966

This repository does not redistribute the article, its supplementary
material, or any non-public data.

## Disclaimer
This is an independent, personal project, created in my own time.

- It is **not affiliated with, endorsed by, or reviewed by** Purdue
  University, the authors of the work cited above, or any of their
  institutions.
- It is **not affiliated with, endorsed by, or representative of my
  employer**. All views, code and results are my own.
- The code is provided "as is", without warranty of any kind
  (see LICENSE).

## Setup
Developed on Ubuntu 26.04 (WSL2) with the system Python 3.

    python3 -m venv .venv
    source .venv/bin/activate
    python -m pip install --upgrade pip
    python -m pip install -r requirements.txt

PyTorch is installed separately with the selector at
https://pytorch.org/get-started/locally/

Further packages (for example Streamlit and QuTiP) are added to
`requirements.txt` when the module that needs them starts.

## License
Code: MIT (see LICENSE).
