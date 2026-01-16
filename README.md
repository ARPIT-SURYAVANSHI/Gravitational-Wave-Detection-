# Gravitational Wave Parameter Estimation using MCMC

## Overview
This project implements a **Bayesian parameter estimation pipeline** to recover the physical parameters of a simulated gravitational wave burst signal embedded in noise. Using a phenomenological waveform model and a **Metropolis–Hastings Markov Chain Monte Carlo (MCMC)** algorithm, the code infers posterior distributions for the signal parameters and quantifies uncertainties.

The project is motivated by techniques used in real gravitational wave data analysis, where weak signals must be extracted from noisy detector data.

---

## Signal Model
The gravitational wave strain is modeled as:

h(t) = α eᵗ [1 − tanh(2(t − β))] sin(γt)

where:
- **α (alpha)** — signal amplitude  
- **β (beta)** — cutoff / turn-off time of the burst  
- **γ (gamma)** — oscillation frequency  

This form captures a rapidly growing burst with a smooth termination and oscillatory structure.

---

## Methodology
- A **Gaussian likelihood** is constructed assuming additive noise in the data.
- Uniform (box) priors are imposed on the parameters:
  - 0 < α < 2  
  - 1 < β < 10  
  - 1 < γ < 20  
- Parameter estimation is performed using a **single-chain Metropolis–Hastings MCMC**.
- Burn-in samples are discarded and the remaining chain is used to:
  - compute posterior statistics,
  - generate trace plots,
  - visualize correlations using corner plots.

---

## Results
The MCMC algorithm converges reliably and recovers the injected signal parameters with high precision.  
The median posterior estimates are:

- **α = 1.40 ± 0.01**  
- **β = 3.94 ± 0.01**  
- **γ = 10.00 ± 0.002**


The best-fit waveform closely matches the underlying signal, demonstrating successful parameter recovery from noisy time-series data.

---
## Repository Structure

```text
.
├── src/
│   └── mcmc_fit.py            # Main MCMC implementation
├── data/
│   └── gw_data.csv            # Simulated gravitational wave strain data
├── plots/
│   ├── best_fit.png           # Best-fit model vs data
│   ├── trace_fit.png          # MCMC trace plots
│   └── corner_fit.png         # Posterior distributions
├── report/
│   └── GW_Parameter_Estimation.pdf
└── README.md
