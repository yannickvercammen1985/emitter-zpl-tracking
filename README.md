# emitter-zpl-tracking

Tools for extracting the zero-phonon line (ZPL) position from noisy,
low-count photoluminescence spectra of single quantum emitters, and for
comparing extraction methods on simulated spectra with a known ground truth.

Methods compared:
- Brightest-pixel (argmax) tracking
- Peak fitting with `scipy.optimize.curve_fit`
- Batched peak fitting on GPU with PyTorch
- A 1D convolutional neural network (PyTorch) trained on simulated spectra

## Stage A progress
| Part | Status | Release |
|---|---|---|
| Spectrum simulator | Planned | – |
| Brightest pixel vs curve_fit | Planned | – |
| GPU batch fit (PyTorch) | Planned | – |
| 1D CNN estimator | Planned | – |
| Streamlit demo | Planned | – |

## Background and acknowledgement
This project was inspired by, and builds on the public work of:

> P. Maan et al., "Anticipating decoherence in quantum systems",
> *Nature Communications* 17, 8239 (2026).
> https://doi.org/10.1038/s41467-026-72829-3

Public data from that study (CC BY 4.0):
https://doi.org/10.5281/zenodo.19455550

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
Install PyTorch with CUDA support using the selector at
https://pytorch.org/get-started/locally/ first, then:

    pip install -r requirements.txt

## License
Code: MIT (see LICENSE).