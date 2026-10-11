# Kernel Regression: Multivariate Data Analysis Coursework

Python implementation of kernel regression (Gaussian process-style prediction) built from scratch, applied to synthetic 1D data and a real 2D surface dataset (Maunga Whau volcano).

**Authors:** Thomas Westby, Tom Hinchey, Will Harvey
**Date:** April 2026

## Overview

Given a kernel function K(x, x′) and observations **z** at sample locations, the optimal predictor at a new point x is

ẑ(x) = k(x)ᵀ K⁻¹ z

with conditional covariance K(x, x′) − k(x)ᵀ K⁻¹ k(x′). This project implements these formulas and uses them to explore how kernel choice and parameters affect predictions and uncertainty.

## What's Covered

### 1. One-dimensional kernel regression
- Optimal prediction, 95% confidence bands and conditional realisations using the Gaussian kernel
- Comparison of **Gaussian**, **Laplace** and **Matérn-3/2** kernels
- Maximum-likelihood estimation (MLE) of the kernel parameter ρ
- Under- and over-fitting illustrated with ρ = 0.05 and ρ = 20
- Extended kernel K = α·exp(−ρ‖x − x′‖²), with joint MLE of α and ρ
- Leave-one-out cross-validation (LOO-CV) as an alternative to MLE
- Sampling distribution of the ρ estimators for 7, 20 and 40 observations

### 2. Volcano data (`DataVolcano50.txt`)
- 50 observations (x, y, z) ∈ [0, 1]² × ℝ
- MLE of ρ for each kernel (≈ 34.22 Gaussian, ≈ 1.81 Laplace, ≈ 4.33 Matérn-3/2)
- Predicted 3D surfaces and 2D contour maps of the upper and lower 95% confidence surfaces

### 3. Extensions
- **Observation noise:** replacing K with K + σ²I, and the effect of σ² on smoothness and confidence bands
- **Finite-dimensional kernels:** polynomial basis kernels K = GGᵀ (degrees 1–3), linking kernel regression to linear regression

## Key Findings

- Kernel choice controls smoothness: the Gaussian kernel gives the smoothest predictions, Matérn-3/2 is slightly rougher, and the Laplace kernel is the roughest.
- ρ controls the length scale. A small ρ underfits and a large ρ overfits.
- α mainly scales the confidence band rather than the shape of the prediction, but α and ρ are not independent when estimated by MLE.
- ρ estimates from 7 points have high variance, and the variance falls as the number of observations grows.
- Observation noise acts as a regulariser: larger σ² gives smoother predictions and wider bands.
- Polynomial kernels are cheap and capture global shape but cannot adapt locally like stationary kernels.

## Repository Structure

```
[your-repo]/
├── [notebook_or_script].ipynb   # main code
├── DataVolcano50.txt            # volcano dataset
├── report.pdf                   # full written report
└── README.md
```

## Getting Started

**Requirements:** Python 3.x, NumPy, SciPy, Matplotlib, Plotly [edit to match your imports]

```bash
git clone https://github.com/[username]/[repo].git
cd [repo]
pip install numpy scipy matplotlib plotly
jupyter notebook [notebook_name].ipynb
```

## Report

The full write-up is in [`report.pdf`](./report.pdf).

## Acknowledgements

Coursework for [Multivariate Data Analysis / Cardiff University], [2026]
